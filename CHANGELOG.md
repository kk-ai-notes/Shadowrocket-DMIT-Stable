# Changelog

## 2026-10-31 — v1

- 新建独立 Shadowrocket 配置项目。
- 使用 Shadowrocket 原生 `DOMAIN-SUFFIX`、`IP-CIDR`、`GEOIP`、`FINAL` 规则。
- 加入中国 IPv4 与 IPv6 地址快照，避免仅依赖 GEOIP/CN。
- 加入 ChatGPT、Claude、Gemini、Google、YouTube、X、GitHub 等代理域名。
- 保留 IPv6，关闭 AAAA 优先，国内直连使用系统 DNS。
- 添加 `build.py` 与 `validate.py`。
- 尚未完成 GitHub HTTPS 发布和 iPhone 实机验收。
- 根据现有 cn-direct.conf 诊断：允许不支持代理 UDP 的请求直连，代理流量屏蔽 QUIC，直连 DNS 失败时允许回退代理；LAN 路由排除；IPv6 网段使用 `IP-CIDR6`。

