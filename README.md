# WordPress 在 Docker Compose 环境中的设置指南

## 介绍

提供了在 Docker Compose 环境中设置和运行 WordPress。使用 Docker Compose 可以简化 WordPress 及其相关服务的管理和部署过程。

## 环境要求

- Docker（已安装）
- Docker Compose（已安装）

## 设置步骤

### 1. 配置环境变量

在项目根目录下找到 `.env` 文件，根据需要修改以下环境变量：

```env
MARIADB_USER=wordpress
MARIADB_DATABASE=wordpress
MARIADB_PASSWORD=your_secure_password
```

**注意**：请将 `your_secure_password` 替换为一个强密码。

### 2. 启动 Docker Compose 服务

在项目根目录下执行以下命令：

```shell
# 拉取最新的 Docker 镜像
docker compose pull

# 在后台启动 Docker 服务
docker compose up -d
```

服务启动后，您可以通过浏览器访问 `http://localhost:8000` 来使用您的 WordPress 网站。

**注意**：如果您修改了端口设置，请使用相应的端口号。

## 管理 Docker 服务

### 停止服务

要停止运行中的 WordPress 服务，请在项目根目录下执行：

```shell
docker compose down
```

### 查看日志

使用以下命令查看 Docker 容器的日志：

```shell
# 查看所有容器的日志
docker compose logs

# 实时查看日志（按 Ctrl+C 退出）
docker compose logs -f
```

### 进入容器

如需访问 WordPress 容器，可以使用以下命令：

```shell
docker compose exec wordpress bash
```

或者：

```shell
docker exec -it <container_name> /bin/bash
```

**注意**：请将 `<container_name>` 替换为实际的 WordPress 容器名称。

## 故障排除

1. **数据库连接错误**：检查 `.env` 文件中的数据库配置是否正确。

2. **权限问题**：确保 WordPress 目录和文件具有正确的权限设置。

3. **端口冲突**：如果 8000 端口已被占用，可以在 `docker-compose.yml` 文件中修改端口映射。
