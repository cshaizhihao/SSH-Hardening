# 🔥 IMPART TCP

> 银趴火山帮 鸡儿硬邦邦

基于 [`chnnic/SSH-Hardening`](https://github.com/chnnic/SSH-Hardening) fork 增强的 VPS 初始化与 TCP 调优脚本。主打：SSH 加固、Fail2ban、防火墙、BBR/FQ、TCP 参数调优、脚本自安装与快速更新。

```text
    ██╗███╗   ███╗██████╗  █████╗ ██████╗ ████████╗    ████████╗ ██████╗██████╗
    ██║████╗ ████║██╔══██╗██╔══██╗██╔══██╗╚══██╔══╝    ╚══██╔══╝██╔════╝██╔══██╗
    ██║██╔████╔██║██████╔╝███████║██████╔╝   ██║          ██║   ██║     ██████╔╝
    ██║██║╚██╔╝██║██╔═══╝ ██╔══██║██╔══██╗   ██║          ██║   ██║     ██╔═══╝
    ██║██║ ╚═╝ ██║██║     ██║  ██║██║  ██║   ██║          ██║   ╚██████╗██║
    ╚═╝╚═╝     ╚═╝╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝          ╚═╝    ╚═════╝╚═╝
```

## ✨ 增强内容

- 🎨 主菜单加入 `IMPART TCP` 艺术字和品牌标语。
- 🧭 保留交互式菜单，新增非交互 CLI 参数。
- 🧪 新增 TCP Doctor：快速检查内核、BBR、FQ、网卡、内存并给建议。
- 🌐 新增三套 TCP 预设：`balanced` / `latency` / `throughput`。
- ☁️ 新增 **Cloudflare DDNS**：支持 A/AAAA、IPv4/IPv6 双栈、橙云代理开关、TTL 配置、暂停/恢复自动更新。
- 📦 优化安装、更新、卸载，支持 `v` / `V` / `vtcp` / `volcano-tcp` 快捷命令。
- 🛡️ TCP 配置写入 `/etc/sysctl.d/99-impart-tcp.conf`，避免直接覆盖 `/etc/sysctl.conf`。
- 🔧 增强兼容性：`mktemp` fallback、OpenVZ/LXC 限速提示、chrony/timesyncd 时间同步优化。

## 🚀 快速运行

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/cshaizhihao/SSH-Hardening/refs/heads/main/SSH-Hardening.sh)
```

## 📦 安装到系统

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/cshaizhihao/SSH-Hardening/refs/heads/main/SSH-Hardening.sh) --install
```

安装后可使用：

```bash
v
V
vtcp
volcano-tcp
```

## 🧪 常用命令

```bash
# 查看帮助
volcano-tcp --help

# 查看版本
volcano-tcp --version

# 查看当前 SSH / BBR / tc / DDNS 状态
volcano-tcp --status

# 运行环境体检与建议
volcano-tcp --doctor

# 查看 TCP 预设说明
volcano-tcp --profiles
```

## 🌐 一键 TCP 调优

```bash
# 均衡模式：多数 VPS / 代理 / 建站 / 日常综合，默认推荐
volcano-tcp --tcp balanced

# 低延迟模式：SSH / 游戏 / 远程桌面 / 小包优先
volcano-tcp --tcp latency

# 高吞吐模式：大带宽 / 高延迟 / 下载上传优先
volcano-tcp --tcp throughput
```

调优配置会写入：

```text
/etc/sysctl.d/99-impart-tcp.conf
```

如已有旧配置，脚本会自动备份同路径历史文件。

## ☁️ Cloudflare DDNS

交互菜单中新增 `d) Cloudflare DDNS`，支持：

- 自动创建/更新 `A` 记录
- 可选自动创建/更新 `AAAA` 记录
- 可选 **仅 IPv4** 或 **IPv4 + IPv6 双栈**
- 可选 **Cloudflare 代理（橙云）开关**
- 自定义 **TTL**
- 手动立即更新
- 查看日志
- 修改配置
- **暂停 / 恢复** 自动更新
- 卸载 DDNS

默认定时任务：

```cron
*/5 * * * * /root/ddns.sh >> /var/log/ddns.log 2>&1
```

相关文件：

```text
/root/ddns.sh
/root/.cf_token
/root/.cf_zone
/var/log/ddns.log
```

## 🧩 功能模块

- SSH 工具集
- Fail2ban 管理
- BBR TCP 调优
- 火山帮智能 TCP 向导
- TCP Doctor 环境体检
- Cloudflare DDNS
- 防火墙管理
- DNS 优化
- 系统换源
- IPv4 / IPv6 配置
- Caddy 管理
- 端口转发
- 时间同步
- Swap 管理
- 脚本管理：安装 / 更新 / 卸载

## 🔄 更新与卸载

```bash
# 更新
volcano-tcp --update

# 卸载
volcano-tcp --uninstall
```

## ⚠️ 注意事项

- TCP 调优需要 root 权限。
- 建议先在测试机验证，再应用到生产环境。
- 如果系统内核不支持 BBR，需要升级内核或切换支持 BBR 的发行版内核。
- `tc` 限速、`initcwnd` 等能力依赖系统权限；LXC/OpenVZ 等容器可能受宿主机限制。
- 开启 Cloudflare 代理（橙云）时，请确认业务确实适合走代理；并非所有端口/协议都适用。
- IPv6 DDNS 依赖服务器本身具备可用公网 IPv6；若无 IPv6，脚本会跳过 AAAA 更新。

## 上游来源

- 原仓库：<https://github.com/chnnic/SSH-Hardening>
- 当前 fork：<https://github.com/cshaizhihao/SSH-Hardening>
