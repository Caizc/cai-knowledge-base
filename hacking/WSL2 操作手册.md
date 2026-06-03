# WSL2 常用操作手册

> WSL2（Windows Subsystem for Linux 2）  
> 适用系统：Windows 10 2004+ / Windows 11  
> 更新日期：2026-06

---

## 目录

1. [安装与初始化](#1-安装与初始化)
2. [发行版管理](#2-发行版管理)
3. [启动与关闭](#3-启动与关闭)
4. [文件系统互访](#4-文件系统互访)
5. [网络配置](#5-网络配置)
6. [资源限制与性能调优](#6-资源限制与性能调优)
7. [GPU 支持](#7-gpu-支持)
8. [WSL 与 Windows 互操作](#8-wsl-与-windows-互操作)
9. [备份与迁移](#9-备份与迁移)
10. [systemd 与服务管理](#10-systemd-与服务管理)
11. [开发环境配置](#11-开发环境配置)
12. [常见问题排查](#12-常见问题排查)
13. [常用命令速查表](#13-常用命令速查表)

---

## 1. 安装与初始化

### 一键安装（推荐）

```powershell
# 以管理员身份运行 PowerShell
# 安装 WSL2 并默认使用 Ubuntu
wsl --install

# 安装完成后重启系统
Restart-Computer
```

> 首次启动时，系统会提示设置 Linux 用户名和密码。

### 手动安装步骤

```powershell
# 1. 启用 WSL 功能
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

# 2. 启用虚拟机平台
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

# 3. 重启系统
Restart-Computer

# 4. 设置 WSL 默认版本为 2
wsl --set-default-version 2

# 5. 安装 Linux 发行版（从 Microsoft Store 或命令行）
wsl --install -d Ubuntu-24.04
```

### 更新 WSL

```powershell
wsl --update                 # 更新到最新版
wsl --version                # 查看当前版本
wsl --status                 # 查看 WSL 状态
```

---

## 2. 发行版管理

### 查看与搜索

```powershell
# 列出已安装的发行版
wsl --list
wsl --list --verbose         # 详细信息（名称、状态、WSL版本）
wsl -l -v                    # 简写

# 列出可安装的发行版
wsl --list --online
wsl -l --online
```

### 安装与卸载

```powershell
# 安装指定发行版
wsl --install -d Ubuntu-24.04
wsl --install -d Debian
wsl --install -d kali-linux
wsl --install -d openSUSE-Leap-15.6

# 卸载发行版（会删除所有数据，不可恢复）
wsl --unregister Ubuntu-24.04
```

### 设置默认发行版

```powershell
# 设置默认发行版
wsl --set-default Ubuntu-24.04
wsl -s Ubuntu-24.04          # 简写
```

### 升级到 WSL2

```powershell
# 将指定发行版升级为 WSL2
wsl --set-version Ubuntu 2

# 查看当前版本
wsl -l -v
```

---

## 3. 启动与关闭

### 启动

```powershell
# 进入默认发行版
wsl

# 进入指定发行版
wsl -d Ubuntu-24.04

# 以指定用户登录
wsl -d Ubuntu-24.04 -u root
wsl -d Ubuntu-24.04 -u myuser

# 在 WSL 中执行单条命令后退出
wsl -d Ubuntu-24.04 -- ls -la /home
wsl -- uname -a
```

### 关闭

```powershell
# 关闭指定发行版
wsl --terminate Ubuntu-24.04
wsl -t Ubuntu-24.04          # 简写

# 关闭所有 WSL 实例及虚拟机
wsl --shutdown

# 在 Linux 内部退出当前会话
exit
```

### 修改默认登录用户

```powershell
# Ubuntu 修改默认用户
ubuntu config --default-user myuser

# 通用方法（适用于其他发行版）
# 编辑 /etc/wsl.conf（见第6节）
```

---

## 4. 文件系统互访

### Windows → Linux

```powershell
# Windows 中访问 WSL 文件系统（资源管理器地址栏输入）
\\wsl$\Ubuntu-24.04\home\username\

# PowerShell 中操作 WSL 文件
Get-ChildItem "\\wsl$\Ubuntu-24.04\home"
Copy-Item "C:\data\file.txt" "\\wsl$\Ubuntu-24.04\home\user\"
```

### Linux → Windows

```bash
# WSL 中访问 Windows 文件（C 盘挂载在 /mnt/c）
ls /mnt/c/Users/
ls /mnt/d/Projects/

# 常用路径映射
# C:\Users\<用户名>\Desktop  →  /mnt/c/Users/<用户名>/Desktop
# D:\Projects               →  /mnt/d/Projects

# 复制 Windows 文件到 Linux 主目录
cp /mnt/c/Users/alice/Downloads/file.zip ~/

# 在 Linux 中创建 Windows 路径软链接
ln -s /mnt/c/Users/alice/Documents ~/win-docs
```

### 挂载配置

WSL2 默认将所有 Windows 磁盘自动挂载到 `/mnt/`。可通过 `/etc/wsl.conf` 自定义：

```ini
# /etc/wsl.conf
[automount]
enabled = true          # 是否自动挂载 Windows 磁盘
root = /mnt/            # 挂载根路径
options = "metadata,umask=22,fmask=11"  # 挂载选项（支持 chmod/chown）
mountFsTab = true       # 是否读取 /etc/fstab

[interop]
appendWindowsPath = true  # 是否将 Windows PATH 加入 Linux PATH
```

> 修改 `/etc/wsl.conf` 后需执行 `wsl --shutdown` 并重启生效。

### 性能建议

| 场景 | 建议 |
|------|------|
| 项目文件在 Linux 内 | 存放在 `~/` 等 Linux 文件系统，读写最快 |
| 需要在两端共享文件 | 存放在 Windows，通过 `/mnt/` 访问 |
| 大量小文件操作（如 node_modules） | 务必放在 Linux 文件系统，性能差异巨大 |

---

## 5. 网络配置

### 基本网络信息

```bash
# WSL 内查看 IP 地址
ip addr show eth0
hostname -I

# 查看 Windows 宿主机 IP（WSL2 的网关）
ip route show | grep default
cat /etc/resolv.conf   # nameserver 即为宿主机 IP

# 从 Windows 获取 WSL IP
wsl hostname -I
```

### 端口访问

```bash
# WSL 内启动服务后，Windows 可通过 localhost 访问（WSL2 自动端口转发）
# 例：在 WSL 启动 Python HTTP 服务
python3 -m http.server 8080
# Windows 浏览器访问 http://localhost:8080 即可
```

```powershell
# 如需从局域网其他设备访问 WSL 服务，需手动配置端口转发
# （以管理员身份运行 PowerShell）

# 添加端口转发（将宿主机 8080 转发到 WSL 的 8080）
$wslIp = (wsl hostname -I).Trim()
netsh interface portproxy add v4tov4 listenport=8080 listenaddress=0.0.0.0 connectport=8080 connectaddress=$wslIp

# 添加防火墙规则
New-NetFirewallRule -DisplayName "WSL2 Port 8080" -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow

# 查看所有端口转发规则
netsh interface portproxy show all

# 删除端口转发
netsh interface portproxy delete v4tov4 listenport=8080 listenaddress=0.0.0.0
```

### DNS 配置

```bash
# 修复 DNS 解析问题
sudo tee /etc/wsl.conf << 'EOF'
[network]
generateResolvConf = false
EOF

sudo tee /etc/resolv.conf << 'EOF'
nameserver 8.8.8.8
nameserver 8.8.4.4
EOF

# 防止被覆盖
sudo chattr +i /etc/resolv.conf
```

### 镜像网络模式（WSL 2.0+）

WSL 2.0+ 支持新的镜像网络模式，让 WSL 与 Windows 共享同一网络接口，解决端口访问和局域网可见性问题。

在 `%USERPROFILE%\.wslconfig` 中配置：

```ini
[wsl2]
networkingMode = mirrored    # 启用镜像网络模式
```

> 需要 WSL 版本 ≥ 2.0.0，执行 `wsl --update` 升级后 `wsl --shutdown` 重启生效。

---

## 6. 资源限制与性能调优

### .wslconfig 配置文件

在 Windows 用户目录下创建 `%USERPROFILE%\.wslconfig`（即 `C:\Users\<用户名>\.wslconfig`）：

```ini
[wsl2]
# 内存限制（默认为系统内存的 50% 或 8GB，取较小值）
memory = 8GB

# CPU 核心数限制（默认使用全部核心）
processors = 4

# 交换空间大小（默认为 memory 的 25%）
swap = 4GB

# 交换文件路径（默认 %USERPROFILE%\AppData\Local\Temp\swap.vhdx）
swapFile = D:\\wsl-swap.vhdx

# 是否启用嵌套虚拟化（运行 Docker、KVM 等需要）
nestedVirtualization = true

# 本地回环（localhost）连接（默认 true）
localhostForwarding = true

# 禁止回收内存（防止 Vmmem 进程不释放内存）
# pageReporting = false

# 网络模式
networkingMode = mirrored

# DNS 隧道
dnsTunneling = true

# 防火墙集成
firewall = true
```

> 修改后执行 `wsl --shutdown` 重启 WSL 生效。

### /etc/wsl.conf 配置文件

在 WSL 内的 `/etc/wsl.conf` 中配置（每个发行版独立）：

```ini
[boot]
# 启用 systemd（WSL 0.67.6+）
systemd = true

# 启动时执行命令
# command = /usr/bin/my-startup-script.sh

[user]
# 默认登录用户
default = myusername

[network]
# 主机名
hostname = my-wsl
# 是否自动生成 /etc/hosts
generateHosts = true
# 是否自动生成 /etc/resolv.conf
generateResolvConf = true

[automount]
enabled = true
root = /mnt/
options = "metadata,umask=22,fmask=11"
mountFsTab = false

[interop]
# 是否允许从 Linux 启动 Windows 进程
enabled = true
# 是否将 Windows PATH 追加到 Linux PATH
appendWindowsPath = true
```

### 内存释放问题

WSL2 的 `Vmmem` 进程有时会持续占用大量内存。缓解方法：

```powershell
# 方法1：关闭所有 WSL 实例释放内存
wsl --shutdown

# 方法2：在 .wslconfig 中禁用内存回报（稳定内存使用）
# pageReporting = false

# 方法3：限制最大内存
# memory = 4GB
```

---

## 7. GPU 支持

### NVIDIA GPU（CUDA）

```powershell
# Windows 宿主机安装支持 WSL2 的 NVIDIA 驱动（≥ 470.76）
# 驱动下载：https://www.nvidia.com/Download/index.aspx
```

```bash
# WSL 内安装 CUDA Toolkit（不需要在 Linux 侧安装驱动）
# 参考：https://developer.nvidia.com/cuda-downloads（选择 WSL-Ubuntu）

# 验证 GPU 是否可用
nvidia-smi
nvcc --version
```

### DirectML（AMD / Intel GPU）

WSL2 通过 DirectML 支持 AMD 和 Intel GPU，主要用于机器学习推理。安装 TensorFlow-DirectML 或 PyTorch-DirectML 即可使用。

---

## 8. WSL 与 Windows 互操作

### 从 Linux 调用 Windows 程序

```bash
# 直接调用 Windows 可执行文件
notepad.exe
explorer.exe .            # 在资源管理器中打开当前目录
cmd.exe /c dir

# 调用 PowerShell
powershell.exe -Command "Get-Date"
powershell.exe -File /mnt/c/scripts/setup.ps1

# 调用 VS Code（需安装 WSL 扩展）
code .
code ~/myproject

# 调用 Windows 版 Git
git.exe status

# 实用示例：用 Windows 默认程序打开文件
wslview file.pdf          # 需安装 wslu 工具包
explorer.exe $(wslpath -w ~/document.pdf)
```

### 从 Windows 调用 Linux 命令

```powershell
# 在 PowerShell 中执行 Linux 命令
wsl ls -la
wsl grep -r "keyword" /home/user/
wsl python3 /home/user/script.py

# 管道互通（Windows → Linux → Windows）
Get-ChildItem | wsl grep "\.txt"
dir | wsl awk '{print $NF}'

# 将 Linux 命令输出赋值给 PowerShell 变量
$result = wsl uname -a
$files  = wsl ls ~/projects
```

### 路径转换

```bash
# Linux 路径 ↔ Windows 路径转换
wslpath -w ~/myfile.txt           # Linux → Windows 路径
wslpath -u 'C:\Users\alice'       # Windows → Linux 路径

# 示例
wslpath -w /home/alice/docs       # → \\wsl.localhost\Ubuntu\home\alice\docs
wslpath -u 'D:\Projects\app'      # → /mnt/d/Projects/app
```

### 环境变量共享

```bash
# Windows 环境变量在 WSL 中通过 WSLENV 共享
# 格式：VAR/标志，标志含义：
#   /p  路径（自动转换格式）
#   /l  路径列表（PATH 类型）
#   /u  仅 Windows→Linux
#   /w  仅 Linux→Windows
```

```powershell
# PowerShell 中设置共享变量
$env:MY_TOKEN = "abc123"
$env:WSLENV   = "MY_TOKEN"    # 将 MY_TOKEN 共享给 WSL
wsl echo '$MY_TOKEN'          # 输出 abc123

# 共享路径类型变量
$env:WIN_PROJECT = "C:\Projects\myapp"
$env:WSLENV = "WIN_PROJECT/p"
wsl echo '$WIN_PROJECT'       # 输出 /mnt/c/Projects/myapp
```

---

## 9. 备份与迁移

### 导出与导入

```powershell
# 导出发行版为 .tar 文件（备份）
wsl --export Ubuntu-24.04 D:\Backup\ubuntu-backup.tar

# 导入发行版（还原或迁移）
wsl --import Ubuntu-Restore D:\WSL\Ubuntu D:\Backup\ubuntu-backup.tar

# 导入后设置默认用户（Ubuntu）
ubuntu config --default-user myusername

# 删除原有发行版，用新的替代
wsl --unregister Ubuntu-24.04
wsl --import Ubuntu-24.04 D:\WSL\Ubuntu D:\Backup\ubuntu-backup.tar
```

### 迁移到其他磁盘

WSL2 默认将虚拟磁盘存在 C 盘，空间不足时可迁移：

```powershell
# 1. 导出
wsl --export Ubuntu-24.04 D:\ubuntu-backup.tar

# 2. 注销原发行版
wsl --unregister Ubuntu-24.04

# 3. 导入到新路径（D:\WSL\Ubuntu 为新安装目录）
wsl --import Ubuntu-24.04 D:\WSL\Ubuntu D:\ubuntu-backup.tar --version 2

# 4. 设置默认用户
ubuntu2404 config --default-user myusername
```

### 压缩虚拟磁盘

WSL2 的 `.vhdx` 文件只增不减，可手动压缩回收空间：

```powershell
# 方法1：使用 wsl 命令（WSL 2.0+）
wsl --manage Ubuntu-24.04 --set-sparse true   # 启用稀疏磁盘

# 方法2：手动压缩（管理员 PowerShell）
# 先在 WSL 内清理磁盘
# sudo fstrim -av  或  sudo dd if=/dev/zero of=/tmp/zero bs=1M ; rm /tmp/zero

wsl --shutdown
$vhdPath = "$env:LOCALAPPDATA\Packages\CanonicalGroupLimited.Ubuntu24.04LTS_79rhkp1fndgsc\LocalState\ext4.vhdx"
Optimize-VHD -Path $vhdPath -Mode Full
```

---

## 10. systemd 与服务管理

WSL 0.67.6+ 支持 systemd，需在 `/etc/wsl.conf` 中启用：

```ini
[boot]
systemd = true
```

```bash
# 重启 WSL 后验证 systemd 是否运行
systemctl --version
ps -p 1 -o comm=           # 输出 systemd 表示成功

# 服务管理
sudo systemctl status nginx
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl enable nginx   # 开机自启
sudo systemctl disable nginx

# 查看所有服务
systemctl list-units --type=service
systemctl list-units --type=service --state=running

# 查看服务日志
journalctl -u nginx
journalctl -u nginx -f         # 实时跟踪
journalctl -u nginx --since "1 hour ago"
```

---

## 11. 开发环境配置

### 更新系统与安装常用工具

```bash
# Ubuntu / Debian
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget git vim unzip build-essential

# 安装 wslu（WSL 工具集，提供 wslview、wslpath 等）
sudo apt install -y wslu
```

### Node.js（nvm）

```bash
# 安装 nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc

# 安装 Node.js
nvm install --lts
nvm use --lts
node -v && npm -v
```

### Python

```bash
# Ubuntu 通常预装 Python3
python3 --version
pip3 --version

# 安装 pip 和 venv
sudo apt install -y python3-pip python3-venv

# 创建虚拟环境
python3 -m venv ~/.venvs/myproject
source ~/.venvs/myproject/bin/activate
```

### Docker（推荐使用 Docker Desktop + WSL2 后端）

```powershell
# Windows 端安装 Docker Desktop 并启用 WSL2 集成
# Docker Desktop → Settings → Resources → WSL Integration → 启用目标发行版
```

```bash
# WSL 内直接使用 docker 命令
docker run hello-world
docker compose up -d
```

若不使用 Docker Desktop，也可在 WSL 内直接安装 Docker Engine：

```bash
# 在 WSL（Ubuntu）内安装 Docker Engine
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
```

### VS Code 集成

```bash
# 在 WSL 内直接启动 VS Code（需 Windows 端安装 VS Code 及 WSL 扩展）
code .                     # 在当前目录打开
code ~/myproject           # 打开指定目录
code ~/.bashrc             # 编辑文件
```

### SSH 配置

```bash
# 生成 SSH 密钥
ssh-keygen -t ed25519 -C "your_email@example.com"

# 启动 ssh-agent 并添加密钥
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 自动启动 ssh-agent（添加到 ~/.bashrc 或 ~/.zshrc）
if [ -z "$SSH_AUTH_SOCK" ]; then
    eval "$(ssh-agent -s)" > /dev/null
    ssh-add ~/.ssh/id_ed25519 2>/dev/null
fi
```

### Zsh + Oh My Zsh

```bash
# 安装 Zsh
sudo apt install -y zsh
chsh -s $(which zsh)

# 安装 Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# 安装常用插件
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# 编辑 ~/.zshrc 启用插件
# plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

---

## 12. 常见问题排查

### WSL 无法启动

```powershell
# 检查 WSL 状态
wsl --status

# 更新 WSL
wsl --update

# 重置网络（管理员 PowerShell）
netsh winsock reset
netsh int ip reset

# 重装 WSL 内核
wsl --update --web-download
```

### 网络不通 / DNS 解析失败

```bash
# 测试网络连通性
ping 8.8.8.8        # 能 ping 通说明网络正常，DNS 有问题
ping google.com     # 如果不通说明 DNS 问题

# 临时修复 DNS
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf

# 永久修复（见第5节 DNS 配置）
```

### 时间不同步

```bash
# WSL2 从休眠恢复后时间可能不同步
sudo hwclock -s
# 或
sudo ntpdate time.windows.com
# 或安装 ntp
sudo apt install -y ntp && sudo ntpdate pool.ntp.org
```

### 文件权限问题（Windows 文件在 Linux 中权限异常）

```bash
# 临时修复：挂载时设置权限
sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata,uid=1000,gid=1000,umask=22,fmask=11

# 永久修复：在 /etc/wsl.conf 中配置
# [automount]
# options = "metadata,umask=22,fmask=11"
```

### Vmmem 内存占用过高

```powershell
# 立即释放：关闭所有 WSL 实例
wsl --shutdown

# 长期解决：限制内存上限，在 .wslconfig 中添加：
# [wsl2]
# memory = 4GB
# pageReporting = false
```

### 无法访问 localhost

```bash
# 检查服务是否绑定到 0.0.0.0（而非 127.0.0.1）
ss -tlnp | grep 8080

# 启动服务时明确绑定地址
python3 -m http.server 8080 --bind 0.0.0.0
```

### 磁盘空间不足

```bash
# WSL 内查看磁盘使用情况
df -h
du -sh ~/*  | sort -hr | head -20   # 主目录各项大小

# 清理 apt 缓存
sudo apt clean
sudo apt autoremove -y

# 清理 Docker 资源
docker system prune -a
```

### 查看 WSL 日志

```powershell
# 查看 WSL 事件日志
Get-WinEvent -LogName "Microsoft-Windows-Subsystem-Linux/Operational" | Select-Object -First 20
```

---

## 13. 常用命令速查表

### Windows PowerShell 端

| 功能 | 命令 |
|------|------|
| 安装 WSL | `wsl --install` |
| 安装指定发行版 | `wsl --install -d Ubuntu-24.04` |
| 列出已安装发行版 | `wsl -l -v` |
| 列出可用发行版 | `wsl -l --online` |
| 进入默认发行版 | `wsl` |
| 进入指定发行版 | `wsl -d Ubuntu-24.04` |
| 以 root 登录 | `wsl -d Ubuntu-24.04 -u root` |
| 关闭指定发行版 | `wsl -t Ubuntu-24.04` |
| 关闭所有 WSL | `wsl --shutdown` |
| 设置默认发行版 | `wsl -s Ubuntu-24.04` |
| 更新 WSL | `wsl --update` |
| 查看 WSL 版本 | `wsl --version` |
| 导出备份 | `wsl --export Ubuntu D:\backup.tar` |
| 导入还原 | `wsl --import Ubuntu D:\WSL D:\backup.tar` |
| 注销发行版 | `wsl --unregister Ubuntu-24.04` |
| 执行 Linux 命令 | `wsl <命令>` |
| 获取 WSL IP | `wsl hostname -I` |

### Linux 端（WSL 内）

| 功能 | 命令 |
|------|------|
| 访问 Windows C 盘 | `ls /mnt/c/` |
| Linux→Windows 路径转换 | `wslpath -w ~/file` |
| Windows→Linux 路径转换 | `wslpath -u 'C:\path'` |
| 在资源管理器打开当前目录 | `explorer.exe .` |
| 用 VS Code 打开当前目录 | `code .` |
| 用 Windows 默认程序打开 | `wslview file.pdf` |
| 查看 WSL IP | `hostname -I` |
| 查看宿主机 IP | `ip route show \| grep default` |
| 查看磁盘使用 | `df -h` |

### 配置文件速查

| 文件 | 位置 | 作用 |
|------|------|------|
| `.wslconfig` | `C:\Users\<用户名>\.wslconfig` | 全局 WSL2 配置（内存、CPU、网络等） |
| `wsl.conf` | `/etc/wsl.conf`（每个发行版内） | 单发行版配置（挂载、用户、启动等） |

---

## 附录：推荐工具与资源

### 推荐安装工具

```bash
# wslu - WSL 工具集（wslview、wslpath、wslfetch 等）
sudo apt install wslu

# 查看 WSL 系统信息
wslfetch

# 用 Windows 默认程序打开文件
wslview document.pdf
wslview https://example.com
```

### Windows Terminal 配置建议

Windows Terminal 是 WSL 的最佳搭配终端，支持多标签、GPU 加速渲染和丰富的自定义选项。可在 Microsoft Store 免费安装。

推荐在 `settings.json` 中为 WSL 配置：
- 默认起始目录设为 `//wsl$/Ubuntu-24.04/home/<用户名>`（避免启动在 Windows 挂载路径）
- 启用亚克力背景或自定义主题

### 参考文档

- WSL 官方文档：https://learn.microsoft.com/zh-cn/windows/wsl/
- .wslconfig 完整参数：https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config
- WSL GitHub：https://github.com/microsoft/WSL

---

*如遇问题可查阅官方文档或执行 `wsl --help`*
