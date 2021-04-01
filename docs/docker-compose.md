# 常用命令

```bash
启动服务
docker-compose up

启动后台服务
docker-compose up -d

停止一个服务
docker-compose stop [service-name]

查看正在运行的服务
docker-compose ps

#进入服务容器
docker-compose exec [service-name] bash

#查看服务运行的log
docker-compose logs -f

删除服务
docker-compose rm

```
# 安装docker-compose

```bash
# 下载安装文件
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# 修改权限
sudo chmod +x /usr/local/bin/docker-compose
# 创建软链
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
# 安装完成，查看版本
docker-compose --version
```
