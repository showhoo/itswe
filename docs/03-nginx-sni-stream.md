# 03 · nginx 443 SNI 分流：一个端口服务多个 HTTPS 站点

> [itswe.com](https://www.itswe.com) 建站文档 · 入口篇。当多个 HTTPS 站点共用一台服务器时，用 nginx `stream` 层的 `ssl_preread` 按 SNI 路由，比"每站一个端口"优雅得多。

## 为什么不用默认方式

常规做法是每个站点一个 `server { listen 443 ssl; }`。这条路完全可行，但当你需要：

- 在同一台服务器上引入**非 HTTP 的 TLS 服务**（未来扩展）
- 让**入口层**独立记录"谁在连哪个域名"（ClientHello 阶段就有 SNI，早于证书终止）
- 站点集群整体内移，入口只做路由

stream + SNI 分流就是更干净的架构。

## 核心配置

入口层（OpenResty 主配置的 `stream` 块）：

```nginx
stream {
    log_format sni '$remote_addr [$time_local] $ssl_preread_server_name $status';
    access_log logs/sni_access.log sni;

    map $ssl_preread_server_name $backend {
        www.itswe.com     127.0.0.1:8443;
        itswe.com         127.0.0.1:8443;
        www.example2.com  127.0.0.1:8443;   # 同机其他站点
        default           127.0.0.1:9443;   # 未来新服务的兜底
    }

    server {
        listen 443;
        proxy_pass $backend;
        proxy_protocol on;              # 向后端传递真实客户端 IP
    }
}
```

站点 vhost 层（不再是 `listen 443`）：

```nginx
server {
    listen 8443 ssl proxy_protocol;     # 注意 proxy_protocol
    server_name www.itswe.com itswe.com;

    # 从 PROXY protocol 还原真实 IP（否则日志全是 127.0.0.1）
    set_real_ip_from 127.0.0.1;
    real_ip_header proxy_protocol;

    ssl_certificate     /path/to/fullchain.pem;
    ssl_certificate_key /path/to/privkey.pem;
    # ... 常规 location 配置
}
```

## 三个必踩的坑

### 1. 改了 stream 配置必须 reload 才生效

`map $ssl_preread_server_name` 加了新路由但没 reload，流量继续走 default。确认方式：看 `sni_access.log` 里新域名的请求落在哪个后端。

```bash
nginx -t && nginx -s reload
```

### 2. PROXY protocol 会污染不接受它的后端

`proxy_protocol on` 后，入口会向前端连接**头部插入 16 字节代理头**。后端 vhost 必须 `listen ... proxy_protocol` 才能正确解析；任何**没开启** proxy_protocol 的后端（包括非 HTTP 服务）都会把这 16 字节当成业务数据——TLS 握手第一字节被污染，直接握手失败 EOF。

**约束：同一个后端端口，要么全带代理头，要么全不带。需要两种时各开一个监听。**

### 3. real_ip 不配，日志全部失真

站点日志会记录 127.0.0.1（stream 转发的地址）。必须 `set_real_ip_from` + `real_ip_header proxy_protocol` 还原。CDN 接入后同理还要处理 `X-Forwarded-For`（见 [04 · CDN](04-cdn-edgeone.md)）。

## sni_access.log 的价值

入口层日志记录每次 TLS 会话的 **来源 IP + SNI + 状态**，按天轮转：

```
1.2.3.4 [05/Sep/2026:10:11:12 +0800] www.itswe.com 200
```

用途：

- 排查爬虫/攻击：真实来源 IP 在证书终止之前就能看到
- 统计各域名的连接构成
- 验证分流规则生效（改配置后第一现场）

---

- 上一篇：[02 · MediaWiki 性能调优](02-mediawiki-performance.md) · 下一篇：[04 · 国内 CDN 接入](04-cdn-edgeone.md)
- 站点入口：<https://www.itswe.com>
