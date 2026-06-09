# Claude Code 操作手册

> 基于官方文档整理，适用于日常开发使用  
> 官方文档：https://docs.anthropic.com/en/docs/claude-code/overview

---

## 目录

1. [简介](#1-简介)
2. [安装与认证](#2-安装与认证)
3. [启动与会话管理](#3-启动与会话管理)
4. [常用工作流](#4-常用工作流)
5. [CLI 命令速查](#5-cli-命令速查)
6. [CLI 标志速查](#6-cli-标志速查)
7. [斜杠命令（Slash Commands）](#7-斜杠命令slash-commands)
8. [配置与设置](#8-配置与设置)
9. [CLAUDE.md 上下文文件](#9-claudemd-上下文文件)
10. [MCP 集成](#10-mcp-集成)
11. [高级功能](#11-高级功能)
12. [常见问题排查](#12-常见问题排查)

---

## 1. 简介

Claude Code 是一个 **AI 驱动的代理式编程工具**，运行在终端中，能够理解整个代码库，通过自然语言完成编程任务。

**主要能力：**
- 读取并理解代码库，跨文件编辑
- 执行终端命令、运行测试、处理 Git 工作流
- 修复 Bug、重构代码、编写测试和文档
- 创建 Pull Request

**可用平台：** 终端 CLI、VS Code、JetBrains、桌面应用、浏览器、Slack

---

## 2. 安装与认证

### 安装

```bash
# npm 安装（推荐）
npm install -g @anthropic-ai/claude-code

# 注意：不要使用 sudo npm install -g（会引起权限问题）

# macOS Homebrew
brew install claude-code

# Windows WinGet
winget install Anthropic.ClaudeCode

# 也支持 apt / dnf / apk（Debian、Fedora、Alpine）
```

### 更新

```bash
# 原生安装（自动后台更新）
claude update

# Homebrew
brew upgrade claude-code

# WinGet
winget upgrade Anthropic.ClaudeCode
```

### 认证登录

```bash
# 使用 Claude 订阅登录（推荐）
claude auth login

# 使用 Anthropic Console API Key 登录
claude auth login --console

# 强制 SSO 认证
claude auth login --sso

# 查看当前认证状态
claude auth status

# 退出登录
claude auth logout

# 检查安装状态
claude doctor
```

**订阅要求：** Claude Pro、Max、Team 或 Enterprise 订阅，或 Anthropic Console 账户。

---

## 3. 启动与会话管理

### 启动会话

```bash
# 进入交互式对话
claude

# 带初始提示启动
claude "解释一下这个项目的架构"

# 非交互模式（执行后退出）
claude -p "解释这个函数的作用"

# 管道输入
cat error.log | claude -p "分析这些错误日志"
cat file.py | claude -p "为这段代码写单元测试"
```

### 恢复会话

```bash
# 继续当前目录最近一次会话
claude --continue
claude -c

# 非交互模式继续会话
claude -c -p "检查是否有类型错误"

# 按 ID 或名称恢复
claude -r "auth-refactor" "继续这个 PR"

# 交互式选择要恢复的会话
claude --resume
```

### 并行会话（Worktrees）

```bash
# 在独立分支上开启并行会话（互不干扰）
claude --worktree feature-auth

# 在另一个终端再开一个并行会话
claude --worktree bugfix-payment
```

### 后台代理

```bash
# 在后台启动任务，立即返回
claude --bg "调查 flaky test 问题"

# 查看所有后台会话
claude agents
claude agents --json

# 挂载到某个后台会话
claude attach 7c5dcf5d

# 停止后台会话
claude stop 7c5dcf5d

# 查看后台会话日志
claude logs 7c5dcf5d

# 重启会话（保留对话历史）
claude respawn 7c5dcf5d

# 删除会话记录
claude rm 7c5dcf5d
```

---

## 4. 常用工作流

### 了解新代码库

```
# 进入项目目录后，依次问：
give me an overview of this codebase
explain the main architecture patterns used here
what are the key data models?
how is authentication handled?
```

### 定位代码

```
find the files that handle user authentication
how do these authentication files work together?
trace the login process from front-end to database
```

### 修复 Bug

```
I'm seeing an error when I run npm test
suggest a few ways to fix the @ts-ignore in user.ts
update user.ts to add the null check you suggested
```

### 代码重构

```
find deprecated API usage in our codebase
suggest how to refactor utils.js to use modern JavaScript features
refactor utils.js to use ES2024 features while maintaining the same behavior
run tests for the refactored code
```

### 编写测试

```
find functions in NotificationsService.swift that are not covered by tests
add tests for the notification service
add test cases for edge conditions in the notification service
run the new tests and fix any failures
```

### 创建 Pull Request

```
summarize the changes I've made to the authentication module
create a pr
enhance the PR description with more context about the security improvements

# 从 PR 恢复会话
claude --from-pr 1234
```

### 处理文档

```
find functions without proper JSDoc comments in the auth module
add JSDoc comments to the undocumented functions in auth.js
improve the generated documentation with more context and examples
```

### 引用文件

```bash
# 引用单个文件（@ 前缀）
Explain the logic in @src/utils/auth.js

# 引用目录
What's the structure of @src/components?

# 引用 MCP 资源
Show me the data from @github:repos/owner/repo/issues
```

### 图片输入

- 拖拽图片到 Claude Code 窗口
- 复制图片后 `Ctrl+V` 粘贴（非 `Cmd+V`）
- 提供图片路径：`Analyze this image: /path/to/image.png`

---

## 5. CLI 命令速查

| 命令 | 说明 | 示例 |
|------|------|------|
| `claude` | 启动交互式会话 | `claude` |
| `claude "query"` | 带初始提示启动 | `claude "explain this project"` |
| `claude -p "query"` | 非交互模式执行后退出 | `claude -p "explain this function"` |
| `cat file \| claude -p "query"` | 处理管道内容 | `cat logs.txt \| claude -p "explain"` |
| `claude -c` | 继续最近一次会话 | `claude -c` |
| `claude -r "<id>" "query"` | 按 ID 恢复会话 | `claude -r "auth-refactor" "Finish PR"` |
| `claude update` | 更新到最新版本 | `claude update` |
| `claude install [version]` | 安装指定版本 | `claude install stable` |
| `claude auth login` | 登录 Anthropic 账户 | `claude auth login --console` |
| `claude auth logout` | 登出 | `claude auth logout` |
| `claude auth status` | 查看认证状态 | `claude auth status` |
| `claude agents` | 查看后台代理会话 | `claude agents --json` |
| `claude attach <id>` | 挂载后台会话 | `claude attach 7c5dcf5d` |
| `claude stop <id>` | 停止后台会话 | `claude stop 7c5dcf5d` |
| `claude logs <id>` | 查看会话日志 | `claude logs 7c5dcf5d` |
| `claude respawn <id>` | 重启会话 | `claude respawn 7c5dcf5d` |
| `claude rm <id>` | 删除会话记录 | `claude rm 7c5dcf5d` |
| `claude mcp` | 管理 MCP 服务器 | — |
| `claude plugin` | 管理插件 | `claude plugin install code-review@...` |
| `claude project purge [path]` | 清除项目本地数据 | `claude project purge ~/work/repo --dry-run` |
| `claude setup-token` | 生成 CI 用长效 token | `claude setup-token` |
| `claude daemon status` | 查看后台守护进程状态 | `claude daemon status` |
| `claude daemon stop --any` | 停止守护进程 | `claude daemon stop --any` |
| `claude doctor` | 检查安装状态 | `claude doctor` |

---

## 6. CLI 标志速查

| 标志 | 说明 | 示例 |
|------|------|------|
| `--add-dir` | 添加额外工作目录 | `--add-dir ../apps ../lib` |
| `--append-system-prompt` | 追加自定义系统提示 | `--append-system-prompt "Always use TypeScript"` |
| `--allowedTools` | 指定无需确认的工具 | `"Bash(git log *)" "Read"` |
| `--bg` | 以后台代理模式启动 | `claude --bg "investigate flaky test"` |
| `--bare` | 最简模式（跳过 hooks/skills/MCP） | `claude --bare -p "query"` |
| `--chrome` | 启用 Chrome 浏览器集成 | `claude --chrome` |
| `--continue` / `-c` | 继续上次会话 | `claude -c` |
| `--resume` / `-r` | 选择或指定会话恢复 | `claude -r "session-name"` |
| `--worktree` | 创建独立 worktree 并行会话 | `claude --worktree feature-x` |
| `--model` | 指定使用的模型 | `claude --model claude-opus-4-8` |
| `--safe-mode` | 禁用所有自定义（调试用） | `claude --safe-mode` |
| `--mcp-config` | 指定 MCP 配置文件 | `claude --mcp-config ./mcp.json` |
| `--system-prompt` | 替换默认系统提示 | `claude --system-prompt "..."` |
| `--system-prompt-file` | 从文件加载系统提示 | `claude --system-prompt-file ./prompt.txt` |

---

## 7. 斜杠命令（Slash Commands）

在交互式会话中输入 `/` 使用：

| 命令 | 说明 |
|------|------|
| `/help` | 查看帮助 |
| `/clear` | 清空对话上下文 |
| `/config` | 打开配置界面 |
| `/model` | 切换模型 |
| `/resume` | 选择恢复历史会话 |
| `/status` | 查看当前会话状态 |
| `/usage` | 查看 token 使用量 |
| `/effort` | 调整响应努力程度 |
| `/compact` | 压缩对话历史以节省上下文 |
| `/memory` | 查看/编辑内存内容 |
| `/loop` | 启用定时循环执行 |
| `/powerup` | 交互式功能演示教程 |
| `/terminal-setup` | 配置终端 |

### 自定义斜杠命令

在项目 `.claude/skills/<name>/SKILL.md` 或个人 `~/.claude/skills/<name>/SKILL.md` 中创建，即可通过 `/<name>` 调用。

```markdown
---
name: review-pr
description: 审查 PR 代码质量和安全性
---

请审查以下 PR 的代码：
1. 检查潜在的安全问题
2. 检查代码风格是否符合项目规范
3. 提出改进建议
```

---

## 8. 配置与设置

### 配置作用域

| 作用域 | 位置 | 适用场景 |
|--------|------|----------|
| **Managed** | 系统级管理文件 | 企业统一策略（IT 部署） |
| **User** | `~/.claude/settings.json` | 个人全局偏好 |
| **Project** | `.claude/settings.json` | 团队共享配置（提交到 Git） |
| **Local** | `.claude/settings.local.json` | 个人本地覆盖（不提交） |

优先级（从高到低）：Managed > 命令行参数 > Local > Project > User

### settings.json 示例

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "permissions": {
    "allow": [
      "Bash(npm run lint)",
      "Bash(npm run test *)",
      "Read(~/.zshrc)"
    ],
    "deny": [
      "Bash(curl *)",
      "Read(./.env)",
      "Read(./secrets/**)"
    ]
  },
  "env": {
    "CLAUDE_CODE_ENABLE_TELEMETRY": "1"
  }
}
```

### 常用环境变量

| 变量 | 说明 |
|------|------|
| `ANTHROPIC_API_KEY` | API Key（使用 Console 认证时） |
| `CLAUDE_CODE_SAFE_MODE` | 设为 `1` 启用安全模式 |
| `CLAUDE_CODE_EFFORT_LEVEL` | 响应努力程度（low/medium/high） |
| `CLAUDE_CODE_DISABLE_BUNDLED_SKILLS` | 设为 `1` 禁用内置 skills |
| `CLAUDE_CODE_SIMPLE` | 设为 `1` 启用简化模式 |

---

## 9. CLAUDE.md 上下文文件

`CLAUDE.md` 是项目级 AI 上下文文件，Claude Code 启动时自动读取。

**位置：**
- `CLAUDE.md`（项目根目录，提交到 Git，团队共享）
- `.claude/CLAUDE.md`（等效位置）
- `~/.claude/CLAUDE.md`（个人全局配置）
- `CLAUDE.local.md`（本地覆盖，不提交）

**推荐内容：**

```markdown
# Bash Commands
- npm run build: 构建项目
- npm run test: 运行测试
- npm run typecheck: 类型检查
- docker-compose up -d: 启动开发环境

# Code Style
- 使用 ES modules（import/export），不用 CommonJS（require）
- 优先解构导入（import { foo } from 'bar'）
- 所有新文件使用 TypeScript

# Architecture
- API 路由在 src/routes/，业务逻辑在 src/services/
- 数据库访问层在 src/db/
- 环境变量通过 src/config.ts 统一管理

# Workflow
- 修改后务必运行 typecheck
- 提交前运行完整测试套件
- 分支命名：feature/xxx, bugfix/xxx, hotfix/xxx
```

**写作建议：**
- 使用陈述句而非命令式（"部署目标是 production" 而非 "你必须..."）
- 保持简洁、人类可读
- 避免使用类似系统指令的语气（会触发 Claude 的提示注入防御）

---

## 10. MCP 集成

MCP（Model Context Protocol）允许 Claude Code 连接外部服务。

```bash
# 查看 MCP 配置
claude mcp list

# 添加 MCP 服务器
claude mcp add <name> <url>

# 在会话中引用 MCP 资源
@github:repos/owner/repo/issues
@slack:channels/general/messages
```

**项目级 MCP 配置**（`.mcp.json`，提交到 Git）：

```json
{
  "mcpServers": {
    "github": {
      "type": "url",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

---

## 11. 高级功能

### 计划模式（Plan Before Editing）

```bash
# 启动时进入计划模式（读文件但不修改磁盘）
claude --permission-mode plan

# 在 Shift+Tab 模式循环中加入 bypassPermissions
claude --allow-dangerously-skip-permissions
```

### 定时/定期任务

| 方案 | 运行位置 | 适合场景 |
|------|----------|----------|
| Routines | Anthropic 托管基础设施 | 机器关机时也需运行的任务 |
| 桌面定时任务 | 本机（桌面应用） | 访问本地文件的任务 |
| GitHub Actions | CI 流水线 | 与仓库事件绑定的任务 |
| `/loop` | 当前 CLI 会话 | 会话内快速轮询 |

### 委托子代理研究

在主会话中启动子代理处理研究任务，保持主上下文干净：

```
请在后台调查 Node.js 18 和 20 在我们项目中的兼容性差异，完成后汇报结果
```

### 管道与脚本集成

```bash
# 批量处理文件
for f in src/**/*.ts; do
  claude -p "为这个文件添加 JSDoc 注释" < "$f" > "${f%.ts}.documented.ts"
done

# CI 中使用（需先生成长效 token）
claude setup-token
claude -p "检查 PR #${PR_NUMBER} 是否有安全问题" --bare
```

---

## 12. 常见问题排查

### 安装问题

```bash
# 检查安装状态和版本
claude doctor

# 权限问题：不要用 sudo，改用 npm prefix
npm config set prefix ~/.npm-global
export PATH="$HOME/.npm-global/bin:$PATH"
npm install -g @anthropic-ai/claude-code
```

### 会话问题

```bash
# 找不到历史会话？
claude --resume  # 交互式选择

# 上下文过长导致性能下降？
/compact         # 在会话中压缩历史
/clear           # 或清空重新开始
```

### 权限问题

```bash
# 查看当前权限设置
claude --permission-mode plan  # 只读，不修改文件

# 临时跳过权限确认（谨慎使用）
claude --allow-dangerously-skip-permissions
```

### 调试模式

```bash
# 禁用所有自定义配置（hooks/skills/MCP）进行调试
claude --safe-mode

# 最简模式启动
claude --bare -p "query"
```

### 清除项目数据

```bash
# 预览要删除的内容
claude project purge ~/work/repo --dry-run

# 确认删除
claude project purge ~/work/repo -y
```

---

*文档更新时间：2026-06*  
*参考来源：https://docs.anthropic.com/en/docs/claude-code/overview*
