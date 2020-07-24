#常用命令

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
