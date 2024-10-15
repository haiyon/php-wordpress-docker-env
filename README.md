# PHP-FPM 和 WordPress Docker 设置

## 简介

提供了使用 Docker Compose 设置和运行自定义 PHP-FPM 环境或 WordPress 的说明。这个设置允许在不修改 Dockerfile 的情况下，轻松地在自定义 PHP 应用程序和 WordPress 之间切换。

## 前提条件

- Docker（已安装）
- Docker Compose（已安装）

## 设置说明

### 1. 配置环境变量

在项目根目录下找到 `.env` 文件，根据需要修改以下环境变量：

```env
MARIADB_USER=wordpress
MARIADB_DATABASE=wordpress
MARIADB_PASSWORD=your_secure_password
```

**注意**：请将 `your_secure_password` 替换为一个强密码。

### 2. 选择 PHP-FPM 或 WordPress

在 `docker-compose.yml` 文件中，您可以选择使用自定义 PHP-FPM 或 WordPress：

### 3. 启动 Docker Compose 服务

在项目根目录下执行以下命令：

```shell
# 拉取最新的 Docker 镜像
docker compose pull

# 在后台启动 Docker 服务
docker compose up -d
```

服务启动后，您可以通过浏览器访问 `http://localhost:8000` 来使用您的网站。

## 管理 Docker 服务

### 停止服务

要停止运行中的服务，请在项目根目录下执行：

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

如需访问 PHP-FPM 或 WordPress 容器，可以使用以下命令：

```shell
# 对于自定义 PHP-FPM
docker compose exec php-fpm sh

# 对于 WordPress
docker compose exec wordpress bash
```

## 自定义 PHP 配置

您可以通过修改 `./php/custom.ini` 文件来自定义 PHP 配置。修改后重启服务以使更改生效：

```shell
docker compose restart php-fpm  # 或 wordpress
```

## 故障排除

1. **数据库连接错误**：检查 `.env` 文件中的数据库配置是否正确。

2. **权限问题**：确保 WordPress 目录和文件具有正确的权限设置。

3. **端口冲突**：如果 8000 端口已被占用，可以在 `docker-compose.yml` 文件中修改端口映射。

4. **PHP 扩展问题**：对于自定义 PHP-FPM 设置中的其他 PHP 扩展，修改 Dockerfile 并重新构建镜像。

## 在 PHP-FPM 和 WordPress 之间切换

要在自定义 PHP-FPM 环境和 WordPress 之间切换：

1. 停止当前服务：`docker compose down`
2. 编辑 `docker-compose.yml` 文件，注释/取消注释相应的服务。
3. 重新启动服务：`docker compose up -d`

在环境之间切换时，请记得适当管理您的源代码和数据库。

> 此说明经过 Claude 润色
