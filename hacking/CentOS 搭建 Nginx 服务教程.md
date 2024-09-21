# 安装 Nginx

* 安装依赖包

```bash
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
```

* 下载并解压安装包（nginx 安装包下载：`https://nginx.org/en/download.html`）

```bash
cd /usr/local
mkdir nginx
cd nginx
wget http://nginx.org/download/nginx-1.27.1.tar.gz
tar -xvf nginx-1.27.1.tar.gz
```

* 编译并安装 nginx

```bash
cd /usr/local/nginx/nginx-1.27.1
./configure --prefix=/usr/local/nginx --with-http_ssl_module
make
make install
```

* 配置 nginx（可选）

```bash
vi /usr/local/nginx/conf/nginx.conf
```

* 管理 nginx

```bash
# 启动 nginx
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
# 关闭 nginx
/usr/local/nginx/sbin/nginx -s stop
# 重启 nginx
/usr/local/nginx/sbin/nginx -s reload
```

* 临时关闭防火墙（可选）

# 设置 Nginx 开机自启动

* 创建 `nginx.service` 文件

```bash
cd /lib/systemd/system
vi nginx.service
```

* 向 `nginx.service` 文件加入以下内容，然后保存

```ini
[Unit]
Description=nginx service
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s quit
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

* 将 nginx 加入开机自启动

```bash
# 设置开机启动
systemctl enable nginx.service
# 关闭开启启动
systemctl disable nginx.service
```

* nginx 服务的启动/停止/查看状态

```bash
systemctl start nginx.service
systemctl stop nginx.service
systemctl restart nginx.service
systemctl status nginx.service
```

-------

**Reference:**

* [Linux 安装 Nginx 详细步骤 - 腾讯云](https://cloud.tencent.com/developer/article/1654844)
* [Nginx 安装及其配置详细教程 - 博客园](https://www.cnblogs.com/lywJ/p/10710361.html)
* [Nginx 安装，目录结构与配置文件详解 - 博客园](https://www.cnblogs.com/liang-io/p/9340335.html)

---

change log: 

	- 创建（2024-01-14）

---



