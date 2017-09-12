# Docker Tips

# Docker 命令大全

[Docker 命令大全](http://www.runoob.com/docker/docker-command-manual.html)

## 容器生命周期管理

```
run
start/stop/restart
kill
rm
pause/unpause
create
exec
```

## 容器操作

```
ps
inspect
top
attach
events
logs
wait
export
port
```

## 容器rootfs命令

```
commit
cp
diff
```

## 镜像仓库

```
login
pull
push
search
```

## 本地镜像管理

```
images
rmi
tag
build
history
save
import
info|version
info
version
```

# Docker Documentation

[Docker Documentation](https://docs.docker.com/)

# macOS install Docker

[Mac 上 Docker 的安装和使用初探](http://blog.devzeng.com/blog/using-docker-on-macos.html)
[macOS 安装 Docker](https://yeasy.gitbooks.io/docker_practice/content/install/mac.html)

# MySQL in Docker

## 运行 Docker 中的 MySQL 容器脚本

```
docker run -d -p 127.0.0.1:3306:3306 \
--name mysql \
-v /Users/zicongcai/04-Dev/docker/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD="123zxc" mysql:latest
```

## 安装 MySQL

[Mac 上 Docker 的安装和使用初探](http://blog.devzeng.com/blog/using-docker-on-macos.html)
[mysql 镜像使用](https://yeasy.gitbooks.io/docker_practice/content/appendix/repo/mysql.html)

### 下载MySQL镜像

```
docker pull mysql
```

### 使用镜像创建并启动容器
Docker以镜像为基础创建启动容器的方式为：

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

启动成功后会在终端输出容器的ID，启动MySQL容器的脚本为：


```
docker run -d -p 127.0.0.1:3306:3306 \
			--name mysql \
			-v /Users/zengjing/docker/mysql/data:/var/lib/mysql \
			-e MYSQL_ROOT_PASSWORD=”123456” mysql:latest
```
可以通过 `docker ps -a` 查看容器运行的情况。

参数说明：

* `-d` 表示容器将以后台模式运行，所有I/O数据只能通过网络资源或者共享卷组来进行交互。
* `-p 127.0.0.1:3306:3306` 将主机（127.0.0.1）的端口3306映射到容器的端口3306中。这样访问主机中的3306端口就等于访问容器中的3306端口。
* `--name mysql`给容器取名为 mysql，这样方便识别。
* `-v /Users/zengjing/docker/mysql/data:/var/lib/mysql` 将本机的文件目录挂载到容器对应的目录（`/var/lib/mysql`）中。这样可以通过数据卷实现容器中数据的持久化。
* `-e MYSQL_ROOT_PASSWORD="123456"`, -e表示设置环境变量，此处设置了mysql的root 用户的访问密码为 123456。
* `mysql:latest` 表示使用 mysql 的最新镜像启动一个容器。

### 使用MySQL

完成上面的步骤之后就可以使用MySQL的客户端工具使用了,连接信息如下：

```
Host: 127.0.0.1
Port: 3306
UserName: root
Password: 123456
```

## use MySQL Workbench in macOS

[Download MySQL Workbench](https://dev.mysql.com/downloads/workbench/)
[Mac 下安装 mysql 服务及基于 workbench 的使用方法](https://my.oschina.net/u/2391658/blog/716741)

# Dockerfile

[使用 Dockerfile 构建 Docker 镜像](http://blog.devzeng.com/blog/build-docker-image-with-dockerfile.html)
[docker 构建 java、tomcat、mysql 生产环境镜像](http://kaimingwan.com/post/rong-qi-yu-rong-qi-yun/dockergou-jian-java-tomcat-mysqlsheng-chan-huan-jing-jing-xiang)

---

change log: 

	- 创建（2017-09-11）

---

