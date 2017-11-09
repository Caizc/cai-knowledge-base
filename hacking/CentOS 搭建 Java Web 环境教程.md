# How to Install MySQL on CentOS 7 - linode

## Install MySQL

* Download and add the repository, then update.

```
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpmsudo rpm -ivh mysql-community-release-el7-5.noarch.rpmyum update
```

* Install MySQL as usual and start the service.

```
sudo yum install mysql-serversudo systemctl start mysqld
```

## Harden MySQL Server

```
sudo mysql_secure_installation
```

## Using MySQL

* Root Login

```
mysql -u root -p
```

* Create a New MySQL User and Database

```
 create database testdb; grant all on testdb.* to 'testuser' identified by 'password';
 exit
```

* Reset the MySQL Root Password

```
$ sudo systemctl stop mysqld$ sudo mysqld_safe --skip-grant-tables &
$ mysql -u root
> use mysql;> update user SET PASSWORD=PASSWORD("password") WHERE USER='root';> flush privileges;> exit
$ sudo systemctl start mysqld
```

# 搭建 Java Web 开发环境 - 腾讯云

## 搭建 Java 开发环境

### 安装 JDK

JDK 是开发 Java 程序必须安装的软件，查看一下 yum 源里面的 JDK（此步骤可省略）：

```
yum list java*
```

选择适合本机的JDK，并安装：

```
yum install java-1.7.0-openjdk* -y
```

安装完成后，查看是否安装成功：

```
java -version
```

### 安装 Tomcat

Tomcat 是一个应用服务器，是开发和调试 jsp 程序的首选，可以利用它来响应 HTML 页面的访问请求。

进入本地文件夹

```
cd /usr/local
```

到官网找到 Tomcat 的下载链接，并下载到服务器中, 这里提供了一个快速下载 Tomcat 的地址：

```
wget https://mc.qcloudimg.com/static/archive/fa66329388f85c08e8d6c12ceb8b2ca3/apache-tomcat-7.0.77.tar.gz
```

解压这个文件夹：

```
tar -zxf apache-tomcat-7.0.77.tar.gz
```

重命名这个文件：

```
mv apache-tomcat-7.0.77 /usr/local/tomcat7
```

进入 bin 文件夹

```
cd /usr/local/tomcat7/bin
```

给这个文件夹下的所有 shell 脚本授予权限：

```
chmod 777 *.sh
```

开启tomcat服务：

```
./startup.sh
```

> 重命名是为了方便后续操作, 并非必须步骤

### 安装 MySQL

使用 yum 安装 MySQL：

```
yum install -y mysql-server mysql mysql-devel
```

安装完成后，启动 MySQL 服务：

```
service mysqld restart
```

设置 MySQL 账户 root 密码：

```
/usr/bin/mysqladmin -u root password 'Password'
```

## 访问 Tomcat

### 访问 Tomcat

此时，访问 `http://<服务器 IP 地址>:8080` 可访问到刚才启动的 Tomcat 的内置示例页面。

## 完成

# Trouble Shooting

* mysqld 服务要在 iptables 服务之后启动，否则将导致 MySQL 的端口无法访问，这种情况下只要重启一下 mysqld 服务即可。

-------

**Reference:**

[搭建 Java Web 开发环境 - 开发者实验室 - 腾讯云](https://cloud.tencent.com/developer/labs/lab/10035)
[How to Install MySQL on CentOS 7](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7)（已保存到印象笔记）

---

change log: 

	- 创建（2017-11-09）

---



