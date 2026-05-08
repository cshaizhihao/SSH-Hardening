# 🔥 IMPART OPS PRO

> 银趴火山帮 鸡儿硬邦邦

**IMPART OPS PRO V3.0.0** 是一个面向 VPS 场景的开荒、加固、网络优化与基础运维脚本。  
项目基于上游 [`chnnic/SSH-Hardening`](https://github.com/chnnic/SSH-Hardening) 深度增强，现已从单一 tcp 调优工具升级为更完整的 **VPS 初始化工具箱**。

适用场景：
- 新机开荒
- SSH 加固
- BBR / tcp 网络优化
- Fail2ban / firewall 基础安全收口
- NAT / 家宽 / 动态公网环境下的 Cloudflare DDNS
- Caddy、swap、时间同步、端口转发等常见运维动作

---

## 版本信息

- **产品名：** IMPART OPS PRO
- **当前版本：** V3.0.0
- **仓库地址：** <https://github.com/cshaizhihao/SSH-Hardening>
- **上游项目：** <https://github.com/chnnic/SSH-Hardening>

---

## 核心特性

### 1. VPS 开荒与安全加固
- SSH 管理
- 端口调整
- 密钥生成与公钥管理
- 登录方式调整
- Fail2ban 管理
- firewall 管理

### 2. 网络优化
- BBR tcp 调优
- 多套预设：`balanced` / `latency` / `throughput`
- tc 限速
- DNS 优化
- IPv4 / IPv6 配置

### 3. NAT / 动态公网场景支持
- Cloudflare DDNS
- 支持 `A` 记录
- 支持 `AAAA` 记录
- 支持 **仅 IPv4** 或 **IPv4 + IPv6 双栈**
- 支持 Cloudflare 代理开关（橙云 / 灰云）
- 支持 TTL 配置
- 支持暂停 / 恢复自动更新
- 针对 cron / crontab 缺失场景做了兼容处理

### 4. 系统与服务运维
- Caddy 管理
- 系统换源
- swap 管理
- 时间同步
- 端口转发

### 5. 使用体验增强
- 主菜单品牌化艺术字
- 交互式菜单 + CLI 参数双模式
- TCP Doctor / 状态速览
- 更适合发行与长期维护的 README 与版本化命名

---

## 快速开始

### 直接运行

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/cshaizhihao/SSH-Hardening/refs/heads/main/SSH-Hardening.sh)
```

### 安装到系统

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/cshaizhihao/SSH-Hardening/refs/heads/main/SSH-Hardening.sh) --install
```

安装后可直接使用以下命令：

```bash
v
V
vtcp
volcano-tcp
```

> 说明：当前为兼容旧使用习惯，命令入口仍保留原有快捷名。

---

## 常用命令

```bash
# 查看帮助
volcano-tcp --help

# 查看版本
volcano-tcp --version

# 查看系统状态速览
volcano-tcp --status

# 运行巡检与建议
volcano-tcp --doctor

# 查看 tcp 调优预设说明
volcano-tcp --profiles
```

---

## 一键 tcp 调优

```bash
# 均衡模式：多数 VPS / 代理 / 建站 / 日常综合，默认推荐
volcano-tcp --tcp balanced

# 低延迟模式：SSH / 游戏 / 远程桌面 / 小包优先
volcano-tcp --tcp latency

# 高吞吐模式：大带宽 / 高延迟 / 下载上传优先
volcano-tcp --tcp throughput
```

配置将写入：

```text
/etc/sysctl.d/99-impart-tcp.conf
```

如存在旧配置，脚本会自动备份。

---

## Cloudflare DDNS

交互菜单内提供 `Cloudflare DDNS` 管理入口，适合：
- NAT 机
- 家宽动态公网 IP
- IPv6 / 双栈环境
- 需要长期保持域名解析同步的 VPS 或边缘节点

支持内容：
- 自动创建 / 更新 `A` 记录
- 自动创建 / 更新 `AAAA` 记录
- IPv4-only / IPv4+IPv6 双栈
- Cloudflare 代理开关
- TTL 配置
- 查看日志
- 手动立即更新
- 修改配置
- 暂停 / 恢复自动更新
- 卸载 DDNS

默认 cron：

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

---

## 交互菜单包含的主要模块

- SSH 工具集
- Fail2ban 管理
- BBR tcp 调优
- Cloudflare DDNS
- 防火墙管理
- DNS 优化
- 系统换源
- IPv4 / IPv6 配置
- Caddy 管理
- 端口转发
- 时间同步
- swap 管理
- 脚本管理（安装 / 更新 / 卸载）

---

## 适用环境说明

推荐环境：
- Debian / Ubuntu
- CentOS / Rocky / AlmaLinux
- Alpine（部分功能已做兼容）

已针对以下情况做过兼容增强：
- 无 `systemd` 环境
- OpenVZ / LXC 受限容器提示
- `mktemp` 行为不一致
- cron / crontab 缺失
- NAT / 动态公网出口 IP 探测容错

---

## 注意事项

- 运行脚本建议使用 `root`。
- 涉及 SSH、firewall、Fail2ban、tcp 参数修改前，建议先在测试机验证。
- 若内核不支持 BBR，需要升级内核或使用支持 BBR 的发行版内核。
- `tc` 限速在部分 OpenVZ / LXC 环境中可能受宿主机限制。
- Cloudflare DDNS 的 IPv6 功能依赖服务器本身具备公网 IPv6。
- 若开启 Cloudflare 代理（橙云），请确认业务协议和端口适合走代理。

---

## 发布说明（V3.0.0）

V3.0.0 是一次定位升级版本，核心变化如下：

- 品牌名升级为 **IMPART OPS PRO**
- 从单一 tcp 调优脚本升级为更完整的 **VPS 开荒脚本**
- Cloudflare DDNS 模块完成整合
- NAT 场景兼容性进一步增强
- 主菜单与状态展示重新打磨
- README 重构为可发行版本文档

---

## License / 来源说明

本项目基于开源上游项目增强而来，保留原始来源信息：
- 上游：<https://github.com/chnnic/SSH-Hardening>
- 当前增强版：<https://github.com/cshaizhihao/SSH-Hardening>
