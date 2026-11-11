# Nextin 分流规则

供 Nextin 订阅覆写使用的 YAML 模板。节点由已有订阅注入，文件不包含订阅地址、密码或节点凭据。

## 固定模板链接

https://raw.githubusercontent.com/chtyyds/nextin-rules/main/nextin.yaml

这是规则模板链接，不是节点订阅。请导入 Nextin 的 YAML 模板／分流规则覆写功能，并关联已有订阅，启用规则模式。具体入口可能随版本变化。

## 默认分流

| 流量 | 默认策略 |
| --- | --- |
| 国内域名、国内 IP | 直连 |
| Bilibili、拼多多、小黑盒 | 已补充相关域名直连，广告追踪规则优先 |
| 国内 AI，如豆包、DeepSeek | 直连 |
| 国外 AI，如 ChatGPT、Claude、Gemini、Copilot、Perplexity、Grok、Cursor | AI服务，默认手动节点 |
| YouTube | 独立组，默认手动节点 |
| Netflix | 独立组，默认手动节点 |
| TikTok | 独立组，默认手动节点 |
| Disney+、HBO、Prime Video、Spotify、Twitch | 其他流媒体，默认手动节点 |
| Apple、iCloud、App Store、Apple TV+ | Apple服务，默认直连，可切代理 |
| 微软、Microsoft 365、OneDrive、Windows、Xbox | 微软服务，默认直连，可切代理；Copilot 优先归 AI |
| GitHub 常规服务、其余未匹配流量 | 节点选择，默认手动节点 |
| 已收录广告及追踪域名 | 拦截，可在广告与追踪组临时改为直连排查误杀 |

所有策略组均为手动选择（`select`），没有自动测速、自动切换或故障回退。香港、日本、美国、新加坡、台湾仅用于按名称筛选节点。

导入或刷新模板后，先进入「手动节点」选择一个真实节点；节点选择、AI 和各流媒体组默认使用此节点。也可在服务策略组选择某个地区，再进入对应地区组手动选择节点。Apple、微软仍默认直连。

「REJECT」表示拒绝连接，初次导入请务必选择真实节点。节点不可用时需要手动更换。AI 和流媒体的可用性、地区解锁需实际验证。

## DNS 与网络

- Fake-IP 使用 `198.18.0.1/16`。
- 国内和节点域名通过国内加密 DNS 直连解析；国外域名通过代理加密 DNS 解析。
- 国内 DNS 为阿里／腾讯，国外 DNS 为 Cloudflare／Google。
- 预置 DNS 服务域名到 IP 的 hosts，减少引导解析依赖；没有公网明文 DNS 回退。
- 本地域名保留系统 DNS，家中 NAS 和 Home Assistant 等局域网地址直连。
- iOS 隧道与 DNS 接管由 Nextin 管理。配置中的 `ipv6: false` 不能阻止隧道外 IPv6；导入后需检查实际 DNS 接管及 IPv6 行为。
- App 自带 DoH、系统描述文件或其他 VPN 可能影响结果，需要设备实测。

## 更新方法

直接修改此仓库 `main` 分支的 `nextin.yaml`。固定模板链接保持不变；修改后在 Nextin 刷新模板并按需重新连接。GitHub Raw 可能存在短暂缓存。

不要将订阅密钥或节点密码提交到公开仓库。

## 规则来源与验证

- 来源：[MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)，`meta` 分支。
- 服务分类、广告追踪及专门补充规则写在 YAML 中，为 2026-11-11 的快照。修改应以当前 `nextin.yaml` 为准。
- 国内域名和 IP 使用两个 MRS 规则集，配置为每天更新；首次使用需要有效节点并可访问 GitHub Raw。
- 初始版本通过 Mihomo v1.19.34 配置解析及 46 个代表域名匹配检查；手动版另检查所有策略组均为 select、引用有效且分流规则及 DNS 未变；尚未实测用户的 Nextin 版本、节点、解锁或 DNS 泄漏。
- 域名拦截不能清除全部广告、YouTube 视频内广告或所有隐私追踪。
