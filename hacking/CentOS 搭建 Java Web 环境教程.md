# How to Install MySQL on CentOS 7 - linode

## Install MySQL

* Download and add the repository, then update.

```sh
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
yum update
```

* Install MySQL as usual and start the service.

```sh
sudo yum install mysql-server
sudo systemctl start mysqld
```

## Harden MySQL Server

```sh
sudo mysql_secure_installation
```

## Using MySQL

* Root Login

```sh
mysql -u root -p
```

* Create a New MySQL User and Database

```sh
 create database testdb;
 grant all on testdb.* to 'testuser' identified by 'password';
 exit
```

* Reset the MySQL Root Password

```sh
$ sudo systemctl stop mysqld
$ sudo mysqld_safe --skip-grant-tables &
$ mysql -u root
> use mysql;
> update user SET PASSWORD=PASSWORD("password") WHERE USER='root';
> flush privileges;
> exit
$ sudo systemctl start mysqld
```

# 搭建 Java Web 开发环境 - 腾讯云

## 搭建 Java 开发环境

* [Linux 下安装 Java 环境的三种方式（tar.gz、rpm、yum）- 博客园](https://www.cnblogs.com/antLaddie/p/17599359.html)

```sh
# 配置 Java 环境变量
# vim /etc/profile
# 在文件的最后加入以下内容，然后执行以下命令让环境变量生效
# source /etc/profile

export JAVA_HOME=/usr/local/jdk-21.0.4
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
```

* [Linux 启动 Java 程序 jar 包 shell 脚本 - 博客园](https://www.cnblogs.com/zhaojinhui/p/17238758.html)

### 安装 JDK

JDK 是开发 Java 程序必须安装的软件，查看一下 yum 源里面的 JDK（此步骤可省略）：

```sh
yum list java*
```

选择适合本机的JDK，并安装：

```sh
yum install java-1.7.0-openjdk* -y
```

安装完成后，查看是否安装成功：

```sh
java -version
```

### 安装 Tomcat

Tomcat 是一个应用服务器，是开发和调试 jsp 程序的首选，可以利用它来响应 HTML 页面的访问请求。

进入本地文件夹

```sh
cd /usr/local
```

到官网找到 Tomcat 的下载链接，并下载到服务器中, 这里提供了一个快速下载 Tomcat 的地址：

```sh
wget https://mc.qcloudimg.com/static/archive/fa66329388f85c08e8d6c12ceb8b2ca3/apache-tomcat-7.0.77.tar.gz
```

解压这个文件夹：

```sh
tar -zxf apache-tomcat-7.0.77.tar.gz
```

重命名这个文件：

```sh
mv apache-tomcat-7.0.77 /usr/local/tomcat7
```

进入 bin 文件夹

```sh
cd /usr/local/tomcat7/bin
```

给这个文件夹下的所有 shell 脚本授予权限：

```sh
chmod 777 *.sh
```

开启tomcat服务：

```sh
./startup.sh
```

> 重命名是为了方便后续操作, 并非必须步骤

### 安装 MySQL

使用 yum 安装 MySQL：

```sh
yum install -y mysql-server mysql mysql-devel
```

安装完成后，启动 MySQL 服务：

```sh
service mysqld restart
```

设置 MySQL 账户 root 密码：

```sh
/usr/bin/mysqladmin -u root password 'Password'
```

## 访问 Tomcat

### 访问 Tomcat

此时，访问 `http://<服务器 IP 地址>:8080` 可访问到刚才启动的 Tomcat 的内置示例页面。

## 完成

# SSL 证书申请与安装 - 腾讯云

* [免费 SSL 证书申请流程 - 腾讯云](https://cloud.tencent.com/document/product/400/6814)
* [如何选择 SSL 证书安装部署类型？- 腾讯云](https://cloud.tencent.com/document/product/400/4143)
* [Nginx 服务器 SSL 证书安装部署 - 腾讯云](https://cloud.tencent.com/document/product/400/35244)
* [Tomcat 服务器 SSL 证书安装部署（JKS 格式）（Linux）- 腾讯云](https://cloud.tencent.com/document/product/400/35224)
* [Tomcat 服务器 SSL 证书安装部署（PFX 格式）- 腾讯云](https://cloud.tencent.com/document/product/400/65706)
* [SSL 证书安装相关 - 腾讯云](https://cloud.tencent.com/document/product/400/61387)
* [无法使用 HTTPS 访问网站 - 腾讯云](https://cloud.tencent.com/document/product/400/53650)

# Trouble Shooting

## 防火墙 iptables 导致无法访问

确保 mysqld 服务在 iptables 服务之后启动，否则将导致 MySQL 的端口无法访问，这种情况下只要重启一下 mysqld 服务即可。

## 内存不足导致自动退出

* 创建用于交换分区的文件

```sh
dd if=/dev/zero of=/mnt/swap bs=1M count=2048
# block_size、number_of_block 大小可以自定义，比如 bs=1M count=2048 代表设置 2G 大小swap 分区
```

* 设置交换分区文件

```sh
mkswap /mnt/swap
```

* 立即启用交换分区文件

```sh
swapon /mnt/swap
# 如果在 /etc/rc.local 中有 swapoff -a 需要修改为 swapon -a
```

* 设置开机时自启用 swap 分区

需要修改文件 /etc/fstab 中的 swap 行：

添加 `/mnt/swap swap swap defaults 0 0`

注：/mnt/swap 路径可以修改，可以根据创建的swap文件具体路径来配置。

* 查看效果

设置后可以执行 `free -m` 命令查看效果

[解决阿里云 VPS 服务器 mysql 自动关闭的问题](https://zhuanlan.zhihu.com/p/24888793)
[Linux服务器mysql,nginx等自动停止的排查,以及解决方法](https://www.jisec.com/linux/302.html)

-------

**Reference:**

[搭建 Java Web 开发环境 - 开发者实验室 - 腾讯云](https://cloud.tencent.com/developer/labs/lab/10035)
[How to Install MySQL on CentOS 7](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7)（已保存到印象笔记）

---

change log: 

	- 创建（2017-11-09）
	- 新增 SSL 证书申请与安装相关内容（2024-01-11）
	- 新增搭建 Java 环境的相关链接（2024-09-02）

---



