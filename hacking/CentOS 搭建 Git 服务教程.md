# CentOS 搭建 Git 服务教程

# 卸载旧版本 git

**必须先卸载系统中旧版本的 git，再安装新版本，避免发生冲突。**

如系统中已安装了旧版本的 git，需要先卸载：

```
$ yum remove git
```

如旧版本是编译安装的，则需要到 /usr/bin 目录下，将所有 git 相关的文件删除：

```
cd /usr/bin
rm -f git*
```

# 下载安装 git

Git 是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

> 此实验以 `CentOS 7.2 x64` 的系统为环境，搭建 git 服务器。

## 安装依赖库和编译工具

为了后续安装能正常进行，我们先来安装一些相关依赖库和编译工具：

```
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
```

安装编译工具：

```
yum install gcc perl-ExtUtils-MakeMaker
```

## 下载 git

选一个目录，用来放下载下来的安装包，这里将安装包放在 `/usr/local/src` 目录里：

```
cd /usr/local/src
```

到官网找一个新版稳定的源码包下载到 `/usr/local/src` 文件夹里：

```
wget https://www.kernel.org/pub/software/scm/git/git-2.14.0.tar.gz
```

## 解压和编译

解压下载的源码包：

```
tar -zvxf git-2.14.0.tar.gz
```

解压后进入 `git-2.14.0` 文件夹：

```
cd git-2.14.0
```

执行编译：

```
make all prefix=/usr/local/git
```

编译完成后, 安装到 `/usr/local/git` 目录下：

```
make install prefix=/usr/local/git
```

# 配置环境变量

## 将 git 目录加入 PATH

将原来的 PATH 指向目录修改为现在的目录：

```
echo 'export PATH=$PATH:/usr/local/git/bin' >> /etc/bashrc
```

生效环境变量：

```
source /etc/bashrc
```

此时我们能查看 git 版本号，说明我们已经安装成功了。

```
git --version
```

# 创建 git 账号密码

## 创建 git 账号

为我们刚刚搭建好的 git 创建一个账号：

```
useradd -m git
```

> 删除用户命令为 `userdel git`，切换用户命令为 `su git`

然后为这个账号设置密码：

```
passwd git
```

> 控制台输入创建密码后，输入您自定义的密码，并二次确认。(*****P)

# 初始化 git 仓库并配置用户权限

## 创建 git 仓库并初始化

我们创建 `/usr/git/repositories` 目录用于存放 git 仓库：

```
mkdir -p /usr/git/repositories
```

创建好后，初始化这个仓库：

```
cd /usr/git/repositories/
git init --bare test.git
```

## 配置用户权限

给 git 仓库目录设置用户和用户组并设置权限：

```
chown -R git:git /usr/git/repositories
chmod -R 755 /usr/git/repositories
// 这两个命令必须在新的仓库创建好之后再执行，否则 git 用户对仓库目录没有写权限。之后再创建新的仓库时，也同样需要对新仓库目录进行 git 用户授权
```

查找 git-shell 所在目录, 编辑 `/etc/passwd` 文件，将最后一行关于 gituser 的登录 shell 配置改为 git-shell 的目录，如下示例代码：

`/etc/passwd`

```
git:x:500:500::/home/git:/usr/local/git/bin/git-shell
```

> 如果原来的用户组为 1000:1000，保留原值即可，不需更改，否则系统找不到用户组
> 如果按照刚才的步骤执行, 这个位置应该是 `/usr/local/git/bin/git-shell`。如果不是，很可能是旧版本的 git 未清理干净，请通过 `which git-shell` 命令查看位置，并清除旧版本的 git
> 安全目的, 限制 git 账号的 ssh 连接只能是登录 `git-shell`

## 为客户端生成 SSH 密钥对

打开 Git Bash 或终端，使用 ssh-keygen 生成 SSH 的公钥和密钥：

```
ssh-keygen -t rsa -C "mailname@gmail.com"
```

> 请修改命令中的用户名为自己的用户名，命令执行的过程中不需要输入任何指令，但需要按三次 Enter

执行完毕后，在当前用户目录的 `.ssh` 目录下，就可以看到生成的密钥对，`id_rsa` 为私钥，`id_rsa.pub` 为公钥。将公钥 `id_rsa.pub` 发送给 Git 服务器管理员，管理员将该公钥添加到 Git 服务器上 `gituser` 用户的 `~/.ssh/authorized_keys` 授权列表中，客户端即可访问 Git 服务器中的仓库。

## 为授权用户添加 SSH 公钥

在 `gituser` 用户目录的 `.ssh` 目录下建立 `authorized_keys` 文件来管理授权用户的 SSH 公钥：

```
# 注意！必须是在 git 用户目录下，而不是 root 目录下
$ cd /home/git
$ mkdir .ssh
$ touch .ssh/authorized_keys
# 为 git 用户的根目录赋予权限 744，注意，如果是 644 的话会导致远程访问无权限
$ chmod -R 744 /home/git
```

向 `authorized_keys` 文件添加（追加）用户的 SSH 公钥（可以添加多个）：

```
$ cat id_rsa_user1.pub >> ~/.ssh/authorized_keys
$ cat id_rsa_user2.pub >> ~/.ssh/authorized_keys
```

## 添加安全组规则或防火墙规则

git 服务默认使用 SSH 的 `22` 号端口进行访问，所以需要确保服务器的安全组规则或 iptables 规则中放开对 `TCP 22` 号端口的访问。

## 使用搭建好的 Git 服务

克隆 test 仓库到本地：

```
cd ~
git clone git@<服务器 IP 地址>:/usr/git/repositories/test.git
```

## 为客户端配置用户名和 Email

```
git config --global user.name "username"
git config --global user.email "email@gmail.com"
```

## 完成

恭喜，Git 服务器搭建完成, 从此以后你可以方便地将你的本地代码提交到 Git 服务器托管了。

# Mac 上搭建 Git 服务器

[Mac环境下搭建Git服务器](http://www.liuchungui.com/2015/10/23/gitzong-jie/)

-------

**Reference:**

[搭建 Git 服务器 - 开发者实验室 - 腾讯云](https://www.qcloud.com/developer/labs/lab/10045)
[向 Git 服务器添加 SSH 公钥](http://www.cnblogs.com/0xcafebabe/p/5234678.html)
[搭建服务器上的GIT并实现自动同步到站点目录](http://blog.csdn.net/baidu_30000217/article/details/51327289)
[服务器上的 Git - 生成 SSH 公钥](https://git-scm.com/book/zh/v1/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E7%94%9F%E6%88%90-SSH-%E5%85%AC%E9%92%A5)

---

change log: 

	- 创建（2017-09-10）
	- 更新（2017-12-26）

---

