# 🔥 火山帮 TCP 调优工具

基于 [`chnnic/SSH-Hardening`](https://github.com/chnnic/SSH-Hardening) fork 增强，定位为 VPS 初始化、SSH 加固、Fail2ban、防火墙与 BBR/TCP 调优的一体化脚本。

> 当前增强版：V2.0 · 火山帮 TCP 调优工具

## ✨ 本次增强方向

- 🎨 **整体界面美化**：主标题、菜单、帮助信息与主页面艺术字统一升级为“火山帮 TCP 调优”风格。
- 🧭 **操作逻辑优化**：保留交互式菜单，同时新增命令行参数与智能向导，适合一键执行和自动化调用。
- 🚀 **运行方式优化**：支持 `--status`、`--tcp`、`--install`、`--update`、`--uninstall` 等非交互模式。
- 📦 **安装 / 卸载优化**：默认安装到 `/usr/local/bin/volcano-tcp`，并创建 `v` / `V` / `vtcp` 快捷命令。
- 🌐 **TCP 调优优化**：新增三套预设：均衡、低延迟、高吞吐，自动备份 sysctl 配置后应用。

## 🚀 快速使用

### 直接运行交互菜单

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/cshaizhihao/SSH-Hardening/refs/heads/main/SSH-Hardening.sh)
```

### 查看帮助

```bash
bash SSH-Hardening.sh --help
```

### 查看当前状态

```bash
bash SSH-Hardening.sh --status
```

### 一键 TCP 调优

```bash
# 均衡模式：多数 VPS / 跨境线路推荐
bash SSH-Hardening.sh --tcp balanced

# 低延迟模式：游戏 / SSH / 交互优先
bash SSH-Hardening.sh --tcp latency

# 高吞吐模式：大带宽 / 高延迟 / 下载上传
bash SSH-Hardening.sh --tcp throughput
```

> `--tcp` 会修改 `/etc/sysctl.conf`，执行前会自动生成备份。

## 📦 安装与卸载

### 安装到系统

```bash
bash SSH-Hardening.sh --install
```

安装后可使用：

```bash
v
V
vtcp
volcano-tcp
```

### 更新

```bash
volcano-tcp --update
```

### 卸载

```bash
volcano-tcp --uninstall
```

## 🧩 功能模块

- SSH 工具集
- Fail2ban 管理
- BBR TCP 调优
- 防火墙管理
- DNS 优化
- 系统换源
- IPv4 / IPv6 配置
- Caddy 管理
- 端口转发
- 时间同步
- Swap 管理
- 脚本自我管理

## ⚠️ 注意事项

- 本仓库只提供脚本，不会自动在你的机器上安装或执行调优。
- TCP 调优需要 root 权限。
- 建议先在测试机验证参数，再应用到生产环境。
- 如果内核不支持 BBR，需要升级内核或切换支持 BBR 的发行版内核。

## 上游来源

- 原仓库：<https://github.com/chnnic/SSH-Hardening>
- 当前 fork：<https://github.com/cshaizhihao/SSH-Hardening>
