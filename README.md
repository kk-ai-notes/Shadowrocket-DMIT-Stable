# Shadowrocket-DMIT-Stable

这是一份面向 iPhone Shadowrocket「配置」模式的国内直连 / 海外代理配置。

## 导入

1. 在 Shadowrocket 当前配置页导出并保留原配置备份。
2. 导入 `DMIT-Stable.conf`，选择你现有的 `DMIT-IPv6-Reality` 节点，不要在配置文件中填写 UUID、Reality 私钥或节点链接。
3. 全局路由选择「配置」，观察日志后再测试应用。

配置把 ChatGPT、Claude、Gemini、Google、YouTube、X、GitHub 等域名放在代理规则前面；中国大陆域名和中国 IPv4/IPv6 地址库走直连；未匹配请求最后走代理。

## DNS / IPv6 设计

配置保留 `ipv6 = true`，但不强制优先 AAAA（`prefer-ipv6 = false`），避免 Wi‑Fi/蜂窝网络切换时 IPv6 路由质量变化导致海外或国内服务抖动。国内直连域名使用系统 DNS（`dns-direct-system = true`）；配置不把所有 DNS 强行改到公共 DNS，也不关闭 IPv6。

## 更新

规则快照在 `sources/`。运行：

```powershell
python build.py
python validate.py
```

脚本只生成不含节点凭证的配置。规则源来自 blackmatrix7/ios_rule_script（Shadowrocket China）和 gaoyifan/china-operator-ip（中国 IPv4/IPv6 地址库），每次更新后必须重新运行静态检查，并在 iPhone 上复测。

## 当前限制

Windows 静态检查不能代替 Shadowrocket 真机测试；本项目未宣称已解决 iPhone 上的长期复发问题，也未验证 UDP/QUIC、DNS 缓存、Wi‑Fi/蜂窝切换后的持续运行。

