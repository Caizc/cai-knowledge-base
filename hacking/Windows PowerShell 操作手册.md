# Windows PowerShell 常用操作手册

> 适用版本：PowerShell 5.1 / PowerShell 7+
> 更新日期：2026-06
>
> [PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/)

---

## 目录

1. [基础概念](#1-基础概念)
2. [帮助系统](#2-帮助系统)
3. [文件与目录操作](#3-文件与目录操作)
4. [文本与内容处理](#4-文本与内容处理)
5. [进程与服务管理](#5-进程与服务管理)
6. [网络操作](#6-网络操作)
7. [用户与权限管理](#7-用户与权限管理)
8. [变量与数据类型](#8-变量与数据类型)
9. [流程控制](#9-流程控制)
10. [管道与过滤](#10-管道与过滤)
11. [函数与脚本](#11-函数与脚本)
12. [错误处理](#12-错误处理)
13. [模块管理](#13-模块管理)
14. [计划任务](#14-计划任务)
15. [注册表操作](#15-注册表操作)
16. [环境变量](#16-环境变量)
17. [常用快捷键与技巧](#17-常用快捷键与技巧)

---

## 1. 基础概念

### Cmdlet 命名规范

PowerShell 命令（Cmdlet）遵循 **动词-名词** 结构：

```powershell
Get-Item       # 获取项目
Set-Item       # 设置项目
New-Item       # 创建项目
Remove-Item    # 删除项目
```

### 常用动词

| 动词 | 说明 |
|------|------|
| `Get` | 获取/查询 |
| `Set` | 设置/修改 |
| `New` | 新建/创建 |
| `Remove` | 删除 |
| `Start` | 启动 |
| `Stop` | 停止 |
| `Test` | 测试/验证 |
| `Invoke` | 调用/执行 |
| `Export` | 导出 |
| `Import` | 导入 |

### 别名（Alias）

```powershell
# 查看所有别名
Get-Alias

# 查看特定命令的别名
Get-Alias -Definition Get-ChildItem

# 常用别名对照
# ls / dir / gci  →  Get-ChildItem
# cd / sl         →  Set-Location
# cat / type / gc →  Get-Content
# rm / del / ri   →  Remove-Item
# cp / copy       →  Copy-Item
# mv / move       →  Move-Item
# echo / write    →  Write-Output
# ps              →  Get-Process
# kill            →  Stop-Process
# cls / clear     →  Clear-Host
```

---

## 2. 帮助系统

```powershell
# 更新帮助文件（需管理员权限）
Update-Help

# 查看命令帮助
Get-Help Get-ChildItem
Get-Help Get-ChildItem -Detailed     # 详细说明
Get-Help Get-ChildItem -Examples     # 仅显示示例
Get-Help Get-ChildItem -Full         # 完整文档
Get-Help Get-ChildItem -Online       # 在线文档

# 模糊搜索命令
Get-Help *network*
Get-Help about_*                     # 查看概念性帮助主题

# 查看命令参数
(Get-Command Get-ChildItem).Parameters.Keys

# 查找包含某关键词的命令
Get-Command *process*
Get-Command -Verb Get                # 按动词筛选
Get-Command -Noun Item               # 按名词筛选
```

---

## 3. 文件与目录操作

### 导航

```powershell
# 查看当前路径
Get-Location           # 或 pwd

# 切换目录
Set-Location C:\Users  # 或 cd C:\Users
Set-Location ..        # 返回上级
Set-Location ~         # 切换到用户主目录

# 查看目录内容
Get-ChildItem                        # 或 ls / dir
Get-ChildItem -Path C:\Windows
Get-ChildItem -Recurse               # 递归列出所有子目录
Get-ChildItem -Filter "*.log"        # 按名称过滤
Get-ChildItem -File                  # 仅列出文件
Get-ChildItem -Directory             # 仅列出目录
Get-ChildItem -Hidden                # 显示隐藏文件
Get-ChildItem | Sort-Object Length -Descending  # 按大小排序
```

### 文件操作

```powershell
# 创建文件
New-Item -Path ".\test.txt" -ItemType File
New-Item -Path ".\test.txt" -ItemType File -Value "Hello, World!"

# 创建目录
New-Item -Path ".\NewFolder" -ItemType Directory
mkdir NewFolder                      # 简写

# 复制
Copy-Item "source.txt" "dest.txt"
Copy-Item "C:\src" "C:\dst" -Recurse  # 复制整个目录

# 移动/重命名
Move-Item "old.txt" "new.txt"
Rename-Item "old.txt" "new.txt"

# 删除
Remove-Item "file.txt"
Remove-Item "folder" -Recurse        # 递归删除目录
Remove-Item "folder" -Recurse -Force # 强制删除（含只读文件）

# 检查是否存在
Test-Path "C:\Windows"
Test-Path ".\file.txt" -PathType Leaf       # 判断是否为文件
Test-Path ".\folder" -PathType Container    # 判断是否为目录
```

### 文件属性

```powershell
# 查看属性
Get-Item "file.txt" | Select-Object Name, Length, LastWriteTime

# 修改属性（只读、隐藏等）
Set-ItemProperty "file.txt" -Name Attributes -Value "ReadOnly"
Set-ItemProperty "file.txt" -Name Attributes -Value "Normal"

# 获取文件大小（MB）
(Get-Item "file.zip").Length / 1MB
```

### 路径处理

```powershell
# 拼接路径
Join-Path "C:\Users" "Public\Documents"

# 分解路径
Split-Path "C:\Windows\System32\cmd.exe" -Parent   # C:\Windows\System32
Split-Path "C:\Windows\System32\cmd.exe" -Leaf     # cmd.exe

# 解析绝对路径
Resolve-Path ".\relative\path"

# 获取临时目录
[System.IO.Path]::GetTempPath()
```

---

## 4. 文本与内容处理

### 读写文件

```powershell
# 读取文件内容
Get-Content "file.txt"
Get-Content "file.txt" -TotalCount 10    # 读取前10行（等同 head）
Get-Content "file.txt" -Tail 10          # 读取后10行（等同 tail）
Get-Content "file.txt" -Encoding UTF8    # 指定编码

# 写入文件
Set-Content "file.txt" "Hello, World!"            # 覆盖写入
Add-Content "file.txt" "New Line"                  # 追加写入
"Line1`nLine2" | Out-File "file.txt" -Encoding UTF8  # 管道写入

# 实时监控文件（类似 tail -f）
Get-Content "log.txt" -Wait
```

### 文本搜索与替换

```powershell
# 搜索包含关键字的行（类似 grep）
Get-Content "log.txt" | Select-String "ERROR"
Select-String -Path "*.log" -Pattern "ERROR"
Select-String -Path "*.log" -Pattern "ERROR" -CaseSensitive   # 区分大小写
Select-String -Path "*.log" -Pattern "ERROR" -NotMatch        # 反向匹配

# 正则搜索
Select-String -Path "access.log" -Pattern "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"

# 文本替换
(Get-Content "file.txt") -replace "old", "new" | Set-Content "file.txt"
(Get-Content "file.txt") -replace "(\d+)", '[$1]' | Set-Content "file.txt"  # 正则替换
```

### 字符串操作

```powershell
$str = "Hello, PowerShell!"

$str.Length                    # 字符串长度
$str.ToUpper()                 # 转大写
$str.ToLower()                 # 转小写
$str.Trim()                    # 去除首尾空白
$str.Split(",")                # 分割字符串
$str.Replace("Hello", "Hi")   # 替换
$str.Contains("Power")        # 是否包含
$str.StartsWith("Hello")      # 是否以...开头
$str.Substring(7, 10)         # 截取子串

# 格式化字符串
"My name is {0}, age {1}" -f "Alice", 30
$name = "Alice"; "Hello, $name!"    # 变量内插
```

---

## 5. 进程与服务管理

### 进程管理

```powershell
# 查看进程
Get-Process
Get-Process -Name "chrome"
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10  # CPU 占用最高的10个

# 启动进程
Start-Process "notepad.exe"
Start-Process "cmd.exe" -ArgumentList "/c dir" -Wait
Start-Process "powershell.exe" -Verb RunAs    # 以管理员身份运行

# 结束进程
Stop-Process -Name "notepad"
Stop-Process -Id 1234
Stop-Process -Name "chrome" -Force

# 等待进程结束
Wait-Process -Name "setup"
```

### 服务管理

```powershell
# 查看服务
Get-Service
Get-Service -Name "wuauserv"           # Windows Update
Get-Service | Where-Object Status -eq "Running"  # 仅运行中的服务

# 启动/停止/重启服务（需管理员权限）
Start-Service -Name "wuauserv"
Stop-Service -Name "wuauserv"
Restart-Service -Name "wuauserv"

# 修改服务启动类型
Set-Service -Name "wuauserv" -StartupType Automatic  # 自动
Set-Service -Name "wuauserv" -StartupType Manual      # 手动
Set-Service -Name "wuauserv" -StartupType Disabled    # 禁用
```

---

## 6. 网络操作

```powershell
# 网络连通性测试（类似 ping）
Test-Connection "google.com"
Test-Connection "8.8.8.8" -Count 4
Test-Connection "192.168.1.1" -Quiet    # 仅返回 True/False

# 查看网络配置
Get-NetIPAddress                          # 所有 IP 地址
Get-NetIPAddress -AddressFamily IPv4      # 仅 IPv4
Get-NetAdapter                            # 网络适配器
Get-NetRoute                              # 路由表
Get-DnsClientServerAddress               # DNS 设置

# HTTP 请求（类似 curl / wget）
Invoke-WebRequest "https://example.com"
Invoke-WebRequest "https://example.com" -OutFile "page.html"  # 下载文件
(Invoke-WebRequest "https://api.example.com/data").Content     # 获取内容

# REST API 调用
Invoke-RestMethod "https://api.example.com/users"
$body = @{ name = "Alice"; age = 30 } | ConvertTo-Json
Invoke-RestMethod "https://api.example.com/users" -Method POST -Body $body -ContentType "application/json"

# 查看端口监听
Get-NetTCPConnection -State Listen
Get-NetTCPConnection -LocalPort 80

# DNS 查询
Resolve-DnsName "google.com"
Resolve-DnsName "google.com" -Type MX    # 查询 MX 记录

# 防火墙规则
Get-NetFirewallRule | Where-Object Enabled -eq True
New-NetFirewallRule -DisplayName "Allow HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
```

---

## 7. 用户与权限管理

```powershell
# 查看当前用户
whoami
[System.Security.Principal.WindowsIdentity]::GetCurrent().Name

# 检查是否管理员
([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)

# 本地用户管理（需管理员权限）
Get-LocalUser                                           # 查看所有本地用户
New-LocalUser -Name "newuser" -Password (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force)
Set-LocalUser -Name "newuser" -FullName "New User"
Remove-LocalUser -Name "newuser"
Enable-LocalUser -Name "newuser"
Disable-LocalUser -Name "newuser"

# 本地组管理
Get-LocalGroup
Get-LocalGroupMember -Group "Administrators"
Add-LocalGroupMember -Group "Administrators" -Member "newuser"
Remove-LocalGroupMember -Group "Administrators" -Member "newuser"

# 文件权限（ACL）
Get-Acl "C:\folder"
$acl = Get-Acl "C:\folder"
$acl | Format-List                    # 详细显示

# 修改文件权限
$acl = Get-Acl "C:\folder"
$rule = New-Object System.Security.AccessControl.FileSystemAccessRule("username", "FullControl", "Allow")
$acl.SetAccessRule($rule)
Set-Acl "C:\folder" $acl

# 执行策略
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned     # 允许本地脚本运行（推荐）
Set-ExecutionPolicy Bypass -Scope Process  # 仅对当前会话生效
```

---

## 8. 变量与数据类型

### 变量基础

```powershell
# 赋值
$name = "Alice"
$age  = 30
$pi   = 3.14159
$flag = $true

# 强类型声明
[string]$str  = "Hello"
[int]$num     = 42
[bool]$flag   = $true
[double]$dbl  = 3.14

# 查看类型
$name.GetType()
$age.GetType().Name

# 特殊变量
$null                   # 空值
$true / $false          # 布尔值
$_                      # 管道当前对象
$PSVersionTable         # PowerShell 版本信息
$env:USERNAME           # 当前用户名
$MyInvocation           # 当前脚本/命令信息
$PSScriptRoot           # 脚本所在目录
```

### 数组

```powershell
# 创建数组
$arr = 1, 2, 3, 4, 5
$arr = @(1, 2, 3)
$arr = @()                       # 空数组

# 访问元素
$arr[0]                          # 第一个元素
$arr[-1]                         # 最后一个元素
$arr[1..3]                       # 切片（索引 1 到 3）

# 数组操作
$arr.Count                       # 元素数量
$arr += 6                        # 追加元素
$arr -contains 3                 # 是否包含
$arr | Measure-Object -Sum       # 求和

# 数组方法
[Array]::Sort($arr)
[Array]::Reverse($arr)
```

### 哈希表

```powershell
# 创建哈希表
$hash = @{
    Name = "Alice"
    Age  = 30
    City = "Beijing"
}

# 访问值
$hash["Name"]
$hash.Name

# 修改/添加
$hash["Email"] = "alice@example.com"
$hash.Remove("City")

# 遍历
$hash.Keys
$hash.Values
$hash.GetEnumerator() | ForEach-Object { "$($_.Key) = $($_.Value)" }

# 有序哈希表（保持插入顺序）
$ordered = [ordered]@{ a = 1; b = 2; c = 3 }
```

---

## 9. 流程控制

### 条件判断

```powershell
# if / elseif / else
if ($age -gt 18) {
    Write-Output "成年"
} elseif ($age -eq 18) {
    Write-Output "刚成年"
} else {
    Write-Output "未成年"
}

# 比较运算符
# -eq  等于       -ne  不等于
# -gt  大于       -lt  小于
# -ge  大于等于   -le  小于等于
# -like  通配符匹配   -notlike  不匹配
# -match 正则匹配    -notmatch 不匹配
# -contains 数组包含  -in 值在数组中

# switch
switch ($day) {
    "Monday"   { "星期一" }
    "Tuesday"  { "星期二" }
    "Saturday" { "周末" }
    "Sunday"   { "周末" }
    default    { "工作日" }
}

# switch 支持正则
switch -Regex ($str) {
    "^\d+"  { "数字开头" }
    "^[a-z]" { "小写字母开头" }
}
```

### 循环

```powershell
# for 循环
for ($i = 0; $i -lt 10; $i++) {
    Write-Output $i
}

# foreach 循环
foreach ($item in $collection) {
    Write-Output $item
}

# ForEach-Object（管道）
1..10 | ForEach-Object { $_ * 2 }
Get-ChildItem | ForEach-Object { $_.Name }

# while 循环
$i = 0
while ($i -lt 5) {
    Write-Output $i
    $i++
}

# do-while
do {
    $input = Read-Host "输入 q 退出"
} while ($input -ne "q")

# 循环控制
break      # 跳出循环
continue   # 跳过当前迭代
return     # 从函数/脚本返回
```

---

## 10. 管道与过滤

### 管道基础

```powershell
# 管道传递对象（不是文本）
Get-Process | Stop-Process
Get-Service | Where-Object { $_.Status -eq "Stopped" }
Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 5
```

### 常用过滤命令

```powershell
# Where-Object（过滤）
Get-Process | Where-Object { $_.CPU -gt 10 }
Get-Process | Where-Object CPU -gt 10            # 简化写法

# Select-Object（选择属性/数量）
Get-Process | Select-Object Name, CPU, ID
Get-Process | Select-Object -First 5
Get-Process | Select-Object -Last 5
Get-Process | Select-Object -Skip 10 -First 5   # 跳过10个取5个
Get-Process | Select-Object Name, @{N="MB"; E={[math]::Round($_.WorkingSet/1MB, 2)}}  # 计算列

# Sort-Object（排序）
Get-Process | Sort-Object CPU
Get-Process | Sort-Object CPU -Descending
Get-ChildItem | Sort-Object LastWriteTime

# Group-Object（分组）
Get-Process | Group-Object Company
Get-ChildItem | Group-Object Extension

# Measure-Object（统计）
Get-Process | Measure-Object CPU -Sum -Average -Maximum -Minimum
Get-Content "file.txt" | Measure-Object -Line -Word -Character

# ForEach-Object（逐项处理）
Get-ChildItem "*.txt" | ForEach-Object {
    $content = Get-Content $_.FullName
    Write-Output "$($_.Name): $($content.Count) 行"
}
```

### 格式化输出

```powershell
# 表格格式
Get-Process | Format-Table Name, CPU, ID -AutoSize

# 列表格式
Get-Process -Name "chrome" | Format-List *

# 宽格式
Get-ChildItem | Format-Wide Name -Column 4

# 导出
Get-Process | Export-Csv "processes.csv" -NoTypeInformation -Encoding UTF8
Get-Process | ConvertTo-Json | Out-File "processes.json"
Get-Process | Export-CliXml "processes.xml"
Import-Csv "processes.csv"              # 导入 CSV
Import-CliXml "processes.xml"           # 导入 XML
```

---

## 11. 函数与脚本

### 函数定义

```powershell
# 基本函数
function Say-Hello {
    Write-Output "Hello, World!"
}
Say-Hello

# 带参数的函数
function Greet {
    param (
        [string]$Name = "World",   # 默认值
        [int]$Times = 1
    )
    for ($i = 0; $i -lt $Times; $i++) {
        Write-Output "Hello, $Name!"
    }
}
Greet -Name "Alice" -Times 3

# 带验证的参数
function Set-Age {
    param (
        [Parameter(Mandatory=$true)]   # 必填参数
        [ValidateRange(0, 150)]        # 范围验证
        [int]$Age
    )
    Write-Output "Age: $Age"
}

# 返回值
function Add-Numbers {
    param ([int]$a, [int]$b)
    return $a + $b
}
$result = Add-Numbers 3 5
```

### 脚本

```powershell
# 创建脚本文件 script.ps1 并运行
.\script.ps1
.\script.ps1 -Param1 "value" -Param2 42

# 脚本头部参数声明
param (
    [string]$InputFile,
    [string]$OutputFile = "output.txt"
)

# 点源（dot-source，加载函数到当前会话）
. .\functions.ps1

# 查看/设置执行策略
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## 12. 错误处理

```powershell
# Try / Catch / Finally
try {
    Get-Content "nonexistent.txt" -ErrorAction Stop
}
catch {
    Write-Error "出错了：$($_.Exception.Message)"
}
finally {
    Write-Output "无论如何都会执行"
}

# 捕获特定异常
try {
    [int]"abc"
}
catch [System.InvalidCastException] {
    Write-Output "类型转换错误"
}
catch {
    Write-Output "其他错误：$_"
}

# ErrorAction 参数
Get-Item "nofile" -ErrorAction SilentlyContinue  # 忽略错误
Get-Item "nofile" -ErrorAction Stop              # 将错误变为异常
Get-Item "nofile" -ErrorAction Continue          # 显示错误但继续（默认）

# 自动变量
$Error[0]                  # 最近一次错误
$?                         # 最后命令是否成功（$true/$false）
$LASTEXITCODE              # 最后外部程序退出码

# 全局错误处理
$ErrorActionPreference = "Stop"    # 所有错误都抛异常
$ErrorActionPreference = "Continue"  # 恢复默认
```

---

## 13. 模块管理

```powershell
# 查看已安装模块
Get-Module -ListAvailable
Get-InstalledModule                     # PowerShellGet 安装的模块

# 查看已加载模块
Get-Module

# 搜索模块（需联网）
Find-Module -Name "*Azure*"
Find-Module -Tag "Security"

# 安装/卸载模块
Install-Module -Name "Posh-Git"
Install-Module -Name "PSReadLine" -Force
Uninstall-Module -Name "Posh-Git"
Update-Module -Name "Posh-Git"

# 导入/移除模块
Import-Module "Posh-Git"
Remove-Module "Posh-Git"

# 常用模块推荐
# PSReadLine       - 命令行编辑增强
# Posh-Git         - Git 集成
# oh-my-posh       - 主题美化
# ImportExcel      - 操作 Excel 文件
# PSWindowsUpdate  - Windows 更新管理
# ActiveDirectory  - AD 管理（需 RSAT）
```

---

## 14. 计划任务

```powershell
# 查看计划任务
Get-ScheduledTask
Get-ScheduledTask -TaskName "WindowsDefender*"

# 创建计划任务
$action  = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File C:\Scripts\backup.ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At "2:00AM"
Register-ScheduledTask -TaskName "DailyBackup" -Action $action -Trigger $trigger -RunLevel Highest

# 修改/删除任务
Set-ScheduledTask -TaskName "DailyBackup" -Trigger $newTrigger
Unregister-ScheduledTask -TaskName "DailyBackup" -Confirm:$false

# 启用/禁用/运行任务
Enable-ScheduledTask  -TaskName "DailyBackup"
Disable-ScheduledTask -TaskName "DailyBackup"
Start-ScheduledTask   -TaskName "DailyBackup"
Stop-ScheduledTask    -TaskName "DailyBackup"

# 常用触发器
New-ScheduledTaskTrigger -Once    -At "10:00AM"
New-ScheduledTaskTrigger -Daily   -At "2:00AM"
New-ScheduledTaskTrigger -Weekly  -DaysOfWeek Monday -At "8:00AM"
New-ScheduledTaskTrigger -AtStartup
New-ScheduledTaskTrigger -AtLogOn
```

---

## 15. 注册表操作

```powershell
# 注册表驱动器（像文件系统一样操作）
# HKLM:  HKEY_LOCAL_MACHINE
# HKCU:  HKEY_CURRENT_USER
# HKCR:  HKEY_CLASSES_ROOT

# 浏览注册表
Set-Location HKLM:\SOFTWARE
Get-ChildItem HKCU:\Software\Microsoft

# 读取值
Get-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run"
(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion").ProductName

# 写入值（需权限）
Set-ItemProperty -Path "HKCU:\Software\MyApp" -Name "Theme" -Value "Dark"
New-ItemProperty -Path "HKCU:\Software\MyApp" -Name "Debug" -Value 1 -PropertyType DWORD

# 创建/删除键
New-Item -Path "HKCU:\Software\MyApp"
Remove-Item -Path "HKCU:\Software\MyApp" -Recurse

# 检查键是否存在
Test-Path "HKCU:\Software\MyApp"
```

---

## 16. 环境变量

```powershell
# 查看环境变量
$env:PATH
$env:USERNAME
$env:COMPUTERNAME
Get-ChildItem Env:               # 列出所有环境变量
Get-ChildItem Env:PATH           # 查看 PATH

# 临时修改（仅当前会话）
$env:MY_VAR = "Hello"
$env:PATH += ";C:\MyTools"       # 追加到 PATH

# 永久修改（系统级）
[System.Environment]::SetEnvironmentVariable("MY_VAR", "Hello", "Machine")   # 系统级
[System.Environment]::SetEnvironmentVariable("MY_VAR", "Hello", "User")      # 用户级
[System.Environment]::GetEnvironmentVariable("MY_VAR", "User")               # 读取

# 删除环境变量
[System.Environment]::SetEnvironmentVariable("MY_VAR", $null, "User")
Remove-Item Env:MY_VAR    # 仅删除当前会话
```

---

## 17. 常用快捷键与技巧

### 控制台快捷键

| 快捷键 | 功能 |
|--------|------|
| `Tab` | 自动补全命令/路径 |
| `Ctrl+Space` | 显示补全列表 |
| `↑ / ↓` | 历史命令浏览 |
| `Ctrl+R` | 搜索历史命令 |
| `Ctrl+C` | 中断当前命令 |
| `Ctrl+L` | 清屏 |
| `Home / End` | 行首/行尾 |
| `Ctrl+← / →` | 按单词移动光标 |
| `F7` | 历史命令窗口 |

### 实用技巧

```powershell
# 多行命令（行末加反引号 `）
Get-ChildItem -Path C:\ `
    -Recurse `
    -Filter "*.log"

# 后台运行
Start-Job -ScriptBlock { Start-Sleep 60; Write-Output "Done" }
Get-Job
Receive-Job -Id 1
Remove-Job -Id 1

# 测量执行时间
Measure-Command { Get-ChildItem -Recurse }

# 剪贴板
Get-Clipboard
Set-Clipboard "Hello"
Get-ChildItem | Set-Clipboard    # 复制命令结果到剪贴板

# 输出到文件同时在屏幕显示
Get-Process | Tee-Object -FilePath "processes.txt"

# 对象转换
$obj | ConvertTo-Json
$json | ConvertFrom-Json
$obj | ConvertTo-Csv
$csv  | ConvertFrom-Csv

# 快速打开资源管理器
explorer .

# 查看 PowerShell 版本
$PSVersionTable.PSVersion

# Profile 配置文件（开机自动加载）
$PROFILE                         # 查看 profile 路径
notepad $PROFILE                 # 编辑 profile

# 计算哈希值
Get-FileHash "file.zip"                   # 默认 SHA256
Get-FileHash "file.zip" -Algorithm MD5
```

### 常用单行脚本示例

```powershell
# 查找大文件（>100MB）
Get-ChildItem C:\ -Recurse -ErrorAction SilentlyContinue |
    Where-Object { $_.Length -gt 100MB } |
    Sort-Object Length -Descending |
    Select-Object FullName, @{N="Size(MB)"; E={[math]::Round($_.Length/1MB,1)}}

# 批量重命名文件
Get-ChildItem "*.txt" | Rename-Item -NewName { $_.Name -replace "old","new" }

# 统计目录大小
Get-ChildItem -Recurse | Measure-Object -Property Length -Sum |
    ForEach-Object { "$([math]::Round($_.Sum/1MB,2)) MB" }

# 查找最近修改的文件
Get-ChildItem -Recurse | Where-Object { $_.LastWriteTime -gt (Get-Date).AddDays(-7) }

# 终止所有 chrome 进程
Get-Process chrome | Stop-Process -Force

# 检查端口占用
netstat -ano | Select-String ":8080"
Get-NetTCPConnection -LocalPort 8080 | Select-Object -ExpandProperty OwningProcess | Get-Process
```

---

## 附录：常用命令速查表

| 功能 | 命令 |
|------|------|
| 当前目录 | `Get-Location` / `pwd` |
| 列出文件 | `Get-ChildItem` / `ls` |
| 切换目录 | `Set-Location` / `cd` |
| 读文件 | `Get-Content` / `cat` |
| 写文件 | `Set-Content` |
| 追加文件 | `Add-Content` |
| 复制 | `Copy-Item` / `cp` |
| 移动 | `Move-Item` / `mv` |
| 删除 | `Remove-Item` / `rm` |
| 新建 | `New-Item` |
| 搜索 | `Select-String` |
| 进程列表 | `Get-Process` / `ps` |
| 结束进程 | `Stop-Process` / `kill` |
| 服务列表 | `Get-Service` |
| 网络测试 | `Test-Connection` |
| HTTP 请求 | `Invoke-WebRequest` |
| 清屏 | `Clear-Host` / `cls` |
| 获取帮助 | `Get-Help` |
| 查找命令 | `Get-Command` |

---

*如有疑问请查阅 `Get-Help <命令名> -Examples`*
