# Nextin 与 Loon 地区分流配置

- [Nextin 地区版](https://raw.githubusercontent.com/chtyyds/nextin-rules/main/nextin-regions.yaml)：作为分流模板导入，关联现有节点订阅。
- [Loon 地区版](https://raw.githubusercontent.com/chtyyds/nextin-rules/main/nextin-loon.conf)：作为远程配置导入，节点订阅在 Loon 内添加。
- [Clash Verge Rev 版](https://github.com/chtyyds/clash-verge-rules)：按独立仓库的说明导入。

各地区保留普通、1.5 倍率和简名直连三类自动测速组。简名直连是节点组，流量仍使用所选代理节点。节点选择首项为故障切换，也可以手动指定节点或地区组。

原网站分流与 anti-AD 订阅保留。Loon 的规则优先级和 DNS 设置与 Nextin 有所不同。
