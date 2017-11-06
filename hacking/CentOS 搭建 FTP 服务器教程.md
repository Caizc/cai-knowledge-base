# 搭建 FTP 文件服务

# 安装并启动 FTP 服务

## 安装 VSFTPD

* 使用 yum 安装 vsftpd：

```
yum install vsftpd -y
```

> vsftpd 是在 Linux 上被广泛使用的 FTP 服务器，根据其[官网介绍][https://security.appspot.com/vsftpd.html]，它可能是 UNIX-like 系统下最安全和快速的 FTP 服务器软件。

## 启动 VSFTPD

安装完成后，启动 FTP 服务：

```
service vsftpd start
```

启动后，可以看到系统已经监听了 21 端口：

```
netstat -nltp | grep 21
```

此时，访问 ftp://<您的 CVM IP 地址> 可浏览机器上的 /var/ftp 目录了。

> FTP 协议默认使用 21 端口作为服务端口

# 配置 FTP 权限

目前 FTP 服务登陆允许匿名登陆，也无法区分用户访问，我们需要配置 FTP 访问权限

## 了解 VSFTP 配置

vsftpd 的配置目录为 `/etc/vsftpd`，包含下列的配置文件：

* vsftpd.conf 为主要配置文件
* ftpusers 配置禁止访问 FTP 服务器的用户列表
* user_list 配置用户访问控制

## 阻止匿名访问和切换根目录、被动模式

匿名访问和切换根目录都会给服务器带来[安全风险]，我们把这两个功能关闭。

编辑 `/etc/vsftpd/vsftpd.conf`，找到下面两处配置并修改：

```
# 禁用匿名用户
anonymous_enable=NO
# 禁止切换根目录
chroot_local_user=YES
```

在 vsftpd.conf 的最后添加 PASV 被动模式的设置：

```
# 启用 PASV 模式
pasv_enable=YES
# PASV 使用的最小端口
pasv_min_port=60000
# PASV 使用的最大端口
pasv_max_port=65534
```

> 以上配置的端口号范围需要在防火墙设置中相应放行，才可保证 FTP 数据传输顺利进行。

编辑完成后，保存配置，重新启动 FTP 服务，如：

```
systemctl restart vsftpd
或
service vsftpd restart
```

> 匿名访问让所有人都可以上传文件到服务器上而无需鉴权，而允许切换根目录则可能产生越权访问问题。

## 创建 FTP 用户

创建一个用户 ftpuser：

```
useradd ftpuser
```

为用户 ftpuser 设置密码：

```
echo "Password" | passwd ftpuser --stdin
```

## 限制该用户仅能通过 FTP 访问

限制用户 ftpuser 只能通过 FTP 访问服务器，而不能直接登录服务器：

```
usermod -s /sbin/nologin ftpuser
```

## 为用户分配主目录

为用户 ftpuser 创建主目录并约定：

* /data/ftp 为主目录, 该目录不可上传文件
* /data/ftp/pub 文件只能上传到该目录下

```
mkdir -p /data/ftp/pub
```

创建登录欢迎文件：

```
echo "Welcome to use FTP service." > /data/ftp/welcome.txt
```

设置访问权限：

```
chmod a-w /data/ftp && chmod 777 -R /data/ftp/pub
```

设置为用户的主目录：

```
usermod -d /data/ftp ftpuser
```

> 用户的主目录是用户通过 FTP 登录后看到的根目录
> 方便用户登录后可以看到欢迎信息，并且确定用户确实登录到了主目录上。

# 访问 FTP 服务

## 通过 Windows 资源管理器访问

Windows 用户可以复制下面的[链接]到资源管理器的地址栏访问：

```
ftp://ftpuser:Password@<您的 CVM IP 地址>
```

## 通过 FTP 客户端工具访问

FTP 客户端工具众多，下面推荐两个常用的：

* WinSCP - Windows 下的 FTP 和 SFTP 连接客户端
* FileZilla - 跨平台的 FTP 客户端，支持 Windows 和 Mac
* ncftp - MacOS 命令行客户端

# 完成

---

change log: 

	- 创建（2017-11-05）

---



