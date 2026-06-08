# Git 操作手册

## 目录

1. [配置](#1-配置)
2. [初始化与克隆](#2-初始化与克隆)
3. [查看状态与日志](#3-查看状态与日志)
4. [暂存与提交](#4-暂存与提交)
5. [分支管理](#5-分支管理)
6. [合并与变基](#6-合并与变基)
7. [远程仓库](#7-远程仓库)
8. [撤销与回退](#8-撤销与回退)
9. [标签](#9-标签)
10. [贮藏（Stash）](#10-贮藏stash)
11. [子模块](#11-子模块)
12. [常用别名配置](#12-常用别名配置)

---

## 1. 配置

```bash
# 设置用户信息（全局）
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# 设置默认编辑器
git config --global core.editor "vim"

# 设置默认分支名
git config --global init.defaultBranch main

# 查看所有配置
git config --list

# 查看某项配置
git config user.name
```

> **作用域优先级**：`--local`（仓库级）> `--global`（用户级）> `--system`（系统级）

---

## 2. 初始化与克隆

```bash
# 在当前目录初始化仓库
git init

# 初始化并指定目录名
git init my-project

# 克隆远程仓库
git clone https://github.com/user/repo.git

# 克隆并指定本地目录名
git clone https://github.com/user/repo.git my-dir

# 浅克隆（只取最近 N 次提交，加速克隆）
git clone --depth 1 https://github.com/user/repo.git

# 克隆指定分支
git clone -b dev https://github.com/user/repo.git
```

---

## 3. 查看状态与日志

```bash
# 查看工作区和暂存区状态
git status

# 简洁格式
git status -s

# 查看提交历史
git log

# 单行简洁格式
git log --oneline

# 图形化分支历史
git log --oneline --graph --all

# 查看某文件的修改历史
git log --follow -p path/to/file

# 查看工作区与暂存区的差异
git diff

# 查看暂存区与最新提交的差异
git diff --staged

# 查看两个提交之间的差异
git diff <commit1> <commit2>
```

---

## 4. 暂存与提交

```bash
# 暂存指定文件
git add file.txt

# 暂存所有变更
git add .

# 交互式暂存（分块选择）
git add -p

# 提交
git commit -m "feat: add login feature"

# 暂存并提交（已追踪文件）
git commit -am "fix: correct typo"

# 修改最近一次提交（未推送）
git commit --amend -m "new message"

# 追加内容到最近一次提交（不改 message）
git add forgotten-file.txt
git commit --amend --no-edit
```

> **提交信息规范（Conventional Commits）**
>
> | 前缀 | 含义 |
> |------|------|
> | `feat` | 新功能 |
> | `fix` | 修复 bug |
> | `docs` | 文档变更 |
> | `style` | 格式调整（不影响逻辑） |
> | `refactor` | 重构 |
> | `test` | 测试相关 |
> | `chore` | 构建/工具链变更 |

---

## 5. 分支管理

```bash
# 查看本地分支
git branch

# 查看所有分支（含远程）
git branch -a

# 创建新分支
git branch feature/login

# 切换分支
git checkout feature/login
# 或（Git 2.23+）
git switch feature/login

# 创建并切换
git checkout -b feature/login
# 或
git switch -c feature/login

# 重命名分支
git branch -m old-name new-name

# 删除已合并的本地分支
git branch -d feature/login

# 强制删除本地分支
git branch -D feature/login

# 删除远程分支
git push origin --delete feature/login
```

---

## 6. 合并与变基

### 合并（Merge）

```bash
# 将 feature 分支合并到当前分支
git merge feature/login

# 禁止快进，保留合并提交
git merge --no-ff feature/login

# 合并时压缩为一个提交
git merge --squash feature/login
```

### 变基（Rebase）

```bash
# 将当前分支变基到 main
git rebase main

# 交互式变基（整理最近 N 次提交）
git rebase -i HEAD~3

# 变基冲突解决后继续
git rebase --continue

# 中止变基
git rebase --abort
```

> **Merge vs Rebase**
>
> | | Merge | Rebase |
> |---|---|---|
> | 历史记录 | 保留完整分叉历史 | 线性整洁 |
> | 适用场景 | 合并到主分支 | 同步主分支最新变更 |
> | 注意事项 | 产生合并提交 | 勿对已推送分支变基 |

### 解决冲突

```bash
# 1. 冲突后查看冲突文件
git status

# 2. 手动编辑冲突文件，移除冲突标记
# <<<<<<< HEAD ... ======= ... >>>>>>> branch

# 3. 标记为已解决
git add resolved-file.txt

# 4. 完成合并或变基
git commit         # merge
git rebase --continue  # rebase
```

---

## 7. 远程仓库

```bash
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add origin https://github.com/user/repo.git

# 修改远程地址
git remote set-url origin https://github.com/user/new-repo.git

# 删除远程仓库
git remote remove origin

# 拉取远程变更（fetch + merge）
git pull

# 只拉取不合并
git fetch origin

# 拉取并变基（保持线性历史）
git pull --rebase

# 推送到远程
git push origin main

# 首次推送并设置追踪
git push -u origin feature/login

# 强制推送（慎用，仅用于个人分支）
git push --force-with-lease
```

---

## 8. 撤销与回退

```bash
# 撤销工作区文件修改（未暂存）
git restore file.txt
# 旧写法
git checkout -- file.txt

# 取消暂存（保留工作区修改）
git restore --staged file.txt
# 旧写法
git reset HEAD file.txt

# 回退到上一个提交（保留工作区改动）
git reset --soft HEAD~1

# 回退到上一个提交（保留工作区，清空暂存区）
git reset --mixed HEAD~1

# 回退并丢弃所有改动（危险）
git reset --hard HEAD~1

# 安全撤销某次提交（生成新提交）
git revert <commit-hash>

# 丢弃工作区所有未追踪文件
git clean -fd
```

> **reset 模式对比**
>
> | 模式 | 暂存区 | 工作区 | 适用场景 |
> |------|--------|--------|----------|
> | `--soft` | 保留 | 保留 | 重新整理提交 |
> | `--mixed`（默认）| 清空 | 保留 | 取消暂存后重新提交 |
> | `--hard` | 清空 | 清空 | 彻底放弃本地修改 |

---

## 9. 标签

```bash
# 查看标签
git tag

# 创建轻量标签
git tag v1.0.0

# 创建附注标签（推荐，含元数据）
git tag -a v1.0.0 -m "Release version 1.0.0"

# 给指定提交打标签
git tag -a v0.9.0 <commit-hash>

# 推送单个标签
git push origin v1.0.0

# 推送所有标签
git push origin --tags

# 删除本地标签
git tag -d v1.0.0

# 删除远程标签
git push origin --delete v1.0.0
```

---

## 10. 贮藏（Stash）

```bash
# 贮藏当前工作区和暂存区
git stash

# 贮藏并附加描述
git stash push -m "WIP: login form"

# 同时贮藏未追踪文件
git stash push -u

# 查看贮藏列表
git stash list

# 恢复最近的贮藏（保留 stash 记录）
git stash apply

# 恢复并删除最近的贮藏
git stash pop

# 恢复指定贮藏
git stash apply stash@{2}

# 删除指定贮藏
git stash drop stash@{0}

# 清空所有贮藏
git stash clear
```

---

## 11. 子模块

```bash
# 添加子模块
git submodule add https://github.com/user/lib.git libs/lib

# 克隆含子模块的仓库
git clone --recurse-submodules https://github.com/user/repo.git

# 初始化并更新已有仓库的子模块
git submodule update --init --recursive

# 更新所有子模块到最新
git submodule update --remote

# 删除子模块
git submodule deinit libs/lib
git rm libs/lib
```

---

## 12. 常用别名配置

在 `~/.gitconfig` 中添加以下内容，提升日常效率：

```ini
[alias]
    st   = status -s
    co   = checkout
    sw   = switch
    br   = branch
    ci   = commit
    lg   = log --oneline --graph --all --decorate
    last = log -1 HEAD --stat
    undo = reset --soft HEAD~1
    wip  = stash push -u -m "WIP"
    unwip = stash pop
```

使用示例：

```bash
git lg        # 图形化历史
git last      # 查看最近一次提交详情
git undo      # 撤销最近一次提交，保留改动
git wip       # 快速贮藏当前工作
```

---

