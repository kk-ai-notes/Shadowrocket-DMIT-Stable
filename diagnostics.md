# 诊断与验证记录

## 已确认

- 规则源文件均通过 HTTPS 下载，HTTP 状态为 200。
- blackmatrix7 Shadowrocket China 源明确将 `China.list` 用作 `RULE-SET`，将 `China_Domain.list` 用作 `DOMAIN-SET`；本配置把快照转换为静态 `DOMAIN-SUFFIX`，不混用这两类远程规则。
- 中国 IPv4 / IPv6 地址快照来自 gaoyifan/china-operator-ip。
- `DMIT-Stable.conf` 静态检查通过：13,385 条规则，其中 IPv4 6,180 条、IPv6 3,480 条。
- 示例域名检查通过：海外 AI/社交/开发域名为 PROXY，微信、抖音、小红书、淘宝、支付宝为 DIRECT。
- 配置中未包含 UUID、Reality 私钥、`vless://` 链接或 `[Proxy]` 节点定义。
- 对比用户提供的 `cn-direct.conf`：其 `udp-policy-not-supported-behaviour = REJECT` 会拒绝不支持代理转发的 UDP；其 `dns-direct-fallback-proxy = false` 会在直连 DNS 失败时不回退；其远程规则未固定版本，且 `.../ChinaIPs/ChinaIPs.list` 当前返回 404。以上是配置层面的风险证据，不等于已证明某一个 App 的全部故障原因。

## 未确认

- Shadowrocket 实机是否接受当前 531 KB 配置。
- iPhone Wi‑Fi 与蜂窝网络切换后的持续稳定性。
- DNS 缓存、系统 DNS、DoH/DoT、SVCB/HTTPS 记录对具体 App 的影响。
- 微信、抖音、小红书、淘宝、支付宝的 UDP/QUIC 行为。
- 连续使用一段时间后是否复发。
- 新配置采用 `udp-policy-not-supported-behaviour = DIRECT` 与 `block-quic = all-proxy`，需要在手机上验证国内 QUIC 是否恢复、海外代理是否仍可用。

## 最少真机测试

导入后分别在 Wi‑Fi、蜂窝网络测试：微信、抖音、小红书、淘宝、支付宝、ChatGPT、Claude、Google、YouTube。每个应用至少检查启动、图片、视频和搜索；切换网络后等待 30 秒再重复。若国内 App 卡顿，先在 Shadowrocket 日志中记录该请求的域名、最终策略和 DNS 结果，再修改规则。

