# mihomo-rules

mihomo (Clash Meta) 自定义规则文件 + VPS 工具脚本备份。

通过 GitHub Actions 自动从私有仓库同步到此公开仓库，供 OpenClash 通过 raw URL 拉取。

## 规则文件

| 文件 | 说明 |
|------|------|
| `Direct.list` | 直连规则（国内域名、IP 段） |
| `ProxyLite.list` | 轻量代理规则 |
| `AI.list` | AI 服务规则（ChatGPT、Claude 等） |
| `Claude.list` | Claude 专用规则（classical 文本，含域名与 API 入站网段） |

`Claude.list` 使用 `behavior: classical` 和 `format: text`，由配置中的 `RULE-SET` 指定代理组。规则包含 GitHub、npm、Google 存储等共享服务，其他应用访问这些相同域名时也会命中。

本版规则于 2026-11-19 核对，依据为 Claude Code 官方网络要求、Anthropic 官方入站 IP 清单、MetaCubeX 的 Anthropic 域名列表，以及 Net.Coffee 参考页中的补充域名。参考页补充项尚未通过本地实际流量核验。

- https://code.claude.com/docs/en/network-config
- https://platform.claude.com/docs/en/api/ip-addresses
- https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/anthropic.list
- https://ip.net.coffee/claude/site.html

### OpenClash 中使用

规则 raw URL 格式：
```
https://raw.githubusercontent.com/joyshan1986/mihomo-rules/main/Direct.list
```

## VPS 工具脚本（备份）

以下脚本从第三方来源备份，防止原始链接失效。

| 文件 | 原始来源 | 说明 |
|------|---------|------|
| `tcpx.sh` | [ylx2016/Linux-NetSpeed](https://github.com/ylx2016/Linux-NetSpeed) | BBR/BBRplus/Lotserver 内核管理脚本 |
| `tools.sh` | [lanziii/bbr-](https://github.com/lanziii/bbr-) | Linux 网络优化脚本（TCP 调优、ulimit、内核转发） |

### 使用方法

```bash
# tcpx.sh — BBR 开启和模式选择（选 11 启用 BBR+FQ）
wget -N --no-check-certificate "https://raw.githubusercontent.com/joyshan1986/mihomo-rules/main/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh

# tools.sh — 网络优化（选 2 TCP调优，选 3 内核转发）
wget -N --no-check-certificate "https://raw.githubusercontent.com/joyshan1986/mihomo-rules/main/tools.sh" && chmod +x tools.sh && ./tools.sh
```
