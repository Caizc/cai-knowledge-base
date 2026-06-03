# Docker 操作手册

> Linux 系统 Docker 常规操作指南
> 适用系统：Ubuntu / CentOS / Debian
>
> [docker docs](https://docs.docker.com/)

---

## 目录

1. [Docker 安装与配置](#一docker-安装与配置)
2. [镜像管理](#二镜像管理)
3. [容器管理](#三容器管理)
4. [网络管理](#四网络管理)
5. [数据卷管理](#五数据卷volume管理)
6. [Dockerfile 构建镜像](#六dockerfile-构建镜像)
7. [Docker Compose](#七docker-compose)
8. [系统清理与维护](#八系统清理与维护)
9. [常见问题与技巧](#九常见问题与技巧)
10. [快速命令速查](#十快速命令速查)

---

## Docker 架构

![docker architecture](https://docs.docker.com/get-started/images/docker-architecture.webp)

------

## 一、Docker 安装与配置

### 1.1 安装 Docker（Ubuntu）

在 Ubuntu 系统上，推荐使用官方脚本或 apt 包管理器安装 Docker Engine：

```bash
# 更新包索引并安装依赖
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

# 添加 Docker 官方 GPG 密钥
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 添加 Docker 软件源
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo $VERSION_CODENAME) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 安装 Docker Engine
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 1.2 安装 Docker（CentOS / RHEL）

```bash
# 安装 yum-utils
sudo yum install -y yum-utils

# 添加 Docker 源
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# 安装 Docker
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 1.3 启动与开机自启

```bash
# 启动 Docker 服务
sudo systemctl start docker

# 设置开机自启
sudo systemctl enable docker

# 验证安装
docker --version
sudo docker run hello-world
```

### 1.4 非 root 用户使用 Docker

将当前用户加入 docker 用户组，避免每次都使用 sudo：

```bash
# 将用户加入 docker 组
sudo usermod -aG docker $USER

# 使配置立即生效（重新登录或执行）
newgrp docker

# 验证
docker ps
```

---

## 二、镜像管理

### 2.1 镜像常用命令

| 命令 | 说明 |
|------|------|
| `docker images` | 列出本地所有镜像 |
| `docker images -a` | 列出所有镜像（含中间层） |
| `docker pull <镜像名>:<标签>` | 从仓库拉取镜像 |
| `docker push <镜像名>:<标签>` | 推送镜像到仓库 |
| `docker rmi <镜像ID/名称>` | 删除镜像 |
| `docker rmi $(docker images -q)` | 删除所有本地镜像 |
| `docker image prune` | 清理未被使用的镜像 |
| `docker image prune -a` | 清理所有未被容器使用的镜像 |
| `docker tag <源> <目标>` | 为镜像打标签 |
| `docker inspect <镜像名>` | 查看镜像详细信息 |
| `docker history <镜像名>` | 查看镜像构建历史 |
| `docker save -o <文件.tar> <镜像名>` | 导出镜像为 tar 文件 |
| `docker load -i <文件.tar>` | 从 tar 文件导入镜像 |

### 2.2 拉取与搜索镜像示例

```bash
# 搜索镜像
docker search nginx

# 拉取最新版本
docker pull nginx

# 拉取指定版本
docker pull nginx:1.25
docker pull ubuntu:22.04

# 查看本地镜像列表
docker images
# 输出格式：REPOSITORY  TAG  IMAGE ID  CREATED  SIZE
```

---

## 三、容器管理

### 3.1 容器生命周期命令

| 命令 | 说明 |
|------|------|
| `docker run <镜像名>` | 创建并启动容器 |
| `docker run -d <镜像名>` | 后台运行容器（detach 模式） |
| `docker run -it <镜像名> /bin/bash` | 交互式运行容器 |
| `docker run --name <名称> <镜像名>` | 指定容器名称 |
| `docker run --rm <镜像名>` | 运行完成后自动删除容器 |
| `docker start <容器ID/名称>` | 启动已停止的容器 |
| `docker stop <容器ID/名称>` | 优雅停止容器（SIGTERM） |
| `docker kill <容器ID/名称>` | 强制停止容器（SIGKILL） |
| `docker restart <容器ID/名称>` | 重启容器 |
| `docker pause <容器ID/名称>` | 暂停容器进程 |
| `docker unpause <容器ID/名称>` | 恢复暂停的容器 |
| `docker rm <容器ID/名称>` | 删除已停止的容器 |
| `docker rm -f <容器ID/名称>` | 强制删除运行中的容器 |
| `docker rm $(docker ps -aq)` | 删除所有已停止的容器 |

### 3.2 查看与监控容器

| 命令 | 说明 |
|------|------|
| `docker ps` | 列出运行中的容器 |
| `docker ps -a` | 列出所有容器（含已停止） |
| `docker ps -q` | 仅显示容器 ID |
| `docker logs <容器ID>` | 查看容器日志 |
| `docker logs -f <容器ID>` | 实时跟踪日志输出 |
| `docker logs --tail 100 <容器ID>` | 查看最近 100 行日志 |
| `docker stats` | 实时查看所有容器资源使用 |
| `docker stats <容器ID>` | 查看指定容器资源使用 |
| `docker top <容器ID>` | 查看容器内进程 |
| `docker inspect <容器ID>` | 查看容器详细配置信息 |
| `docker diff <容器ID>` | 查看容器文件系统变更 |

### 3.3 容器交互操作

| 命令 | 说明 |
|------|------|
| `docker exec -it <容器ID> /bin/bash` | 进入运行中的容器 |
| `docker exec <容器ID> <命令>` | 在容器内执行命令 |
| `docker attach <容器ID>` | 附加到容器主进程 |
| `docker cp <容器ID>:<路径> <本地路径>` | 从容器复制文件到宿主机 |
| `docker cp <本地路径> <容器ID>:<路径>` | 从宿主机复制文件到容器 |
| `docker export -o file.tar <容器ID>` | 导出容器文件系统 |
| `docker import file.tar <镜像名>` | 从 tar 导入为镜像 |

### 3.4 常用 run 参数说明

```bash
# 端口映射：-p 宿主机端口:容器端口
docker run -d -p 8080:80 nginx

# 数据卷挂载：-v 宿主机路径:容器路径
docker run -d -v /data/html:/usr/share/nginx/html nginx

# 环境变量：-e
docker run -d -e MYSQL_ROOT_PASSWORD=123456 mysql:8

# 资源限制：限制 CPU 和内存
docker run -d --cpus="1.5" --memory="512m" nginx

# 自动重启策略
docker run -d --restart=always nginx
docker run -d --restart=unless-stopped nginx

# 组合使用示例
docker run -d \
  --name my-nginx \
  -p 80:80 \
  -v /data/html:/usr/share/nginx/html \
  --restart=always \
  nginx:latest
```

---

## 四、网络管理

### 4.1 网络常用命令

| 命令 | 说明 |
|------|------|
| `docker network ls` | 列出所有网络 |
| `docker network create <网络名>` | 创建自定义 bridge 网络 |
| `docker network create --driver overlay <名>` | 创建 overlay 网络（Swarm） |
| `docker network inspect <网络名>` | 查看网络详情 |
| `docker network rm <网络名>` | 删除网络 |
| `docker network prune` | 删除所有未使用的网络 |
| `docker network connect <网络> <容器>` | 将容器连接到网络 |
| `docker network disconnect <网络> <容器>` | 将容器从网络断开 |

### 4.2 网络使用示例

```bash
# 创建自定义网络
docker network create my-network

# 在指定网络中运行容器
docker run -d --name app --network my-network nginx
docker run -d --name db --network my-network mysql:8

# 容器之间可通过名称互相访问
# 在 app 容器中可以通过 "db" 主机名访问数据库

# 查看网络详情
docker network inspect my-network
```

---

## 五、数据卷（Volume）管理

### 5.1 Volume 常用命令

| 命令 | 说明 |
|------|------|
| `docker volume create <卷名>` | 创建数据卷 |
| `docker volume ls` | 列出所有数据卷 |
| `docker volume inspect <卷名>` | 查看卷详情 |
| `docker volume rm <卷名>` | 删除数据卷 |
| `docker volume prune` | 删除所有未使用的数据卷 |

### 5.2 Volume 挂载方式对比

```bash
# 方式一：具名卷（推荐用于持久化数据）
docker volume create mydata
docker run -d -v mydata:/var/lib/mysql mysql:8

# 方式二：绑定挂载（Bind Mount，宿主机目录映射）
docker run -d -v /host/data:/container/data nginx

# 方式三：tmpfs 挂载（仅存内存，容器停止即消失）
docker run -d --tmpfs /tmp nginx

# 只读挂载
docker run -d -v /host/config:/etc/nginx:ro nginx
```

---

## 六、Dockerfile 构建镜像

### 6.1 Dockerfile 常用指令

| 指令 | 说明 |
|------|------|
| `FROM` | 指定基础镜像 |
| `RUN` | 在构建过程中执行命令 |
| `CMD` | 容器启动时默认执行的命令（可被覆盖） |
| `ENTRYPOINT` | 容器启动入口（不易被覆盖） |
| `COPY` | 从构建上下文复制文件到镜像 |
| `ADD` | 复制文件（支持 URL 和解压 tar） |
| `ENV` | 设置环境变量 |
| `ARG` | 定义构建时变量 |
| `EXPOSE` | 声明容器监听的端口 |
| `WORKDIR` | 设置工作目录 |
| `USER` | 指定运行用户 |
| `VOLUME` | 声明挂载点 |
| `LABEL` | 为镜像添加元数据标签 |

### 6.2 Dockerfile 示例（Node.js 应用）

```dockerfile
# 使用官方 Node.js 镜像
FROM node:20-alpine

# 设置工作目录
WORKDIR /app

# 先复制依赖文件（利用构建缓存）
COPY package*.json ./

# 安装依赖
RUN npm ci --only=production

# 复制源代码
COPY . .

# 声明端口
EXPOSE 3000

# 以非 root 用户运行（安全最佳实践）
USER node

# 启动应用
CMD ["node", "server.js"]
```

### 6.3 构建命令

```bash
# 在 Dockerfile 所在目录构建
docker build -t my-app:1.0 .

# 指定 Dockerfile 路径
docker build -f /path/to/Dockerfile -t my-app:1.0 .

# 不使用缓存重新构建
docker build --no-cache -t my-app:latest .

# 多阶段构建（减小最终镜像体积）
# 在 Dockerfile 中使用多个 FROM 指令

# 查看构建历史
docker history my-app:1.0
```

---

## 七、Docker Compose

### 7.1 Compose 常用命令

| 命令 | 说明 |
|------|------|
| `docker compose up` | 创建并启动所有服务 |
| `docker compose up -d` | 后台启动所有服务 |
| `docker compose up --build` | 重新构建镜像后启动 |
| `docker compose down` | 停止并删除容器、网络 |
| `docker compose down -v` | 同时删除数据卷 |
| `docker compose start` | 启动已创建的服务 |
| `docker compose stop` | 停止运行中的服务 |
| `docker compose restart` | 重启服务 |
| `docker compose ps` | 查看服务状态 |
| `docker compose logs` | 查看所有服务日志 |
| `docker compose logs -f <服务名>` | 实时查看指定服务日志 |
| `docker compose exec <服务> bash` | 进入服务容器 |
| `docker compose pull` | 拉取所有服务镜像 |
| `docker compose build` | 构建服务镜像 |
| `docker compose config` | 验证并查看配置 |
| `docker compose scale <服务>=3` | 扩展服务实例数 |

### 7.2 docker-compose.yml 示例（Web + DB）

```yaml
version: "3.9"

services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html:ro
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - app
    networks:
      - frontend

  app:
    build: ./app
    environment:
      - NODE_ENV=production
      - DB_HOST=db
      - DB_PASSWORD=${DB_PASSWORD}
    depends_on:
      db:
        condition: service_healthy
    networks:
      - frontend
      - backend

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_PASSWORD}
      MYSQL_DATABASE: myapp
    volumes:
      - dbdata:/var/lib/mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      interval: 10s
      timeout: 5s
      retries: 5
    networks:
      - backend

volumes:
  dbdata:

networks:
  frontend:
  backend:
```

---

## 八、系统清理与维护

### 8.1 清理命令

| 命令 | 说明 |
|------|------|
| `docker system df` | 查看 Docker 磁盘使用情况 |
| `docker system prune` | 清理所有未使用资源（容器/网络/镜像） |
| `docker system prune -a` | 清理所有未使用资源（含镜像） |
| `docker system prune -a --volumes` | 同时清理数据卷（谨慎） |
| `docker container prune` | 删除所有已停止的容器 |
| `docker image prune -a` | 删除所有未被使用的镜像 |
| `docker volume prune` | 删除未被使用的数据卷 |
| `docker network prune` | 删除未被使用的网络 |

### 8.2 日志管理

```bash
# 限制容器日志大小（在 docker run 时指定）
docker run -d \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  nginx

# 全局配置（编辑 /etc/docker/daemon.json）
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}

# 修改后重启 Docker
sudo systemctl restart docker
```

### 8.3 Docker 服务管理

```bash
# 查看 Docker 服务状态
sudo systemctl status docker

# 查看 Docker 守护进程信息
docker info

# 查看 Docker 版本
docker version

# 重启 Docker 服务
sudo systemctl restart docker
```

---

## 九、常见问题与技巧

### 9.1 常用快捷技巧

- 使用 `--rm` 参数让测试容器运行完后自动删除，保持环境整洁
- 使用 `.dockerignore` 文件排除不需要的文件，加快构建速度
- 多阶段构建（Multi-stage build）可大幅减少生产镜像体积
- 优先使用具名卷（Named Volume）而非绑定挂载来持久化数据库数据
- 生产环境容器应设置 `--restart=unless-stopped` 或 `--restart=always`
- 使用 `docker stats` 监控容器资源，避免内存溢出（OOM）
- 同一业务的多个容器应放在同一自定义网络中，用服务名通信

### 9.2 常用排查命令

```bash
# 查看容器实时日志
docker logs -f --tail 50 <容器ID>

# 查看容器内进程
docker exec -it <容器ID> ps aux

# 检查容器网络连通性
docker exec -it <容器ID> curl http://other-container

# 查看容器环境变量
docker exec <容器ID> env

# 以 root 身份进入容器排查
docker exec -it -u root <容器ID> /bin/bash

# 查看容器 IP 地址
docker inspect -f "{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" <容器ID>
```

---

## 十、快速命令速查

| 命令 | 说明 |
|------|------|
| `docker pull nginx` | 拉取 nginx 镜像 |
| `docker run -d -p 80:80 nginx` | 后台运行 nginx，映射 80 端口 |
| `docker exec -it <ID> bash` | 进入容器 Shell |
| `docker logs -f <ID>` | 实时查看容器日志 |
| `docker stop <ID>` | 优雅停止容器 |
| `docker rm <ID>` | 删除容器 |
| `docker rmi <镜像名>` | 删除镜像 |
| `docker system prune` | 清理未使用资源 |
| `docker compose up -d` | 后台启动 Compose 服务 |
| `docker compose down` | 停止并删除 Compose 服务 |
| `docker stats` | 实时查看资源占用 |
| `docker system df` | 查看磁盘使用情况 |

---

