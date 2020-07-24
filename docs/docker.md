# docker

## docker修改镜像

将文件/etc/docker/daemon.json修改为一下内容：

  ```json
  {
    "registry-mirrors": ["https://registry.docker-cn.com"]
  }
  ```

重启docker

  ```shell
  systemctl restart docker
  ```

## 构建镜像

```shell script
// -t : 镜像名 . :镜像上下文
docker build -t image-name .

// -t : 镜像名  -f:指定Dockerfile . :镜像上下文
docker build -t image-name -f Dockerfile.one .

//从 Git repo 中构建
docker build https://github.com/twang2218/gitlab-ce-zh.git#:11.1

//从tar包构建
docker build http://server/context.tar.gz

```


## 保存/载入镜像

```shell script
//保存镜像为文件 -o 指定保存的镜像名 ,save-file-name.tar 保存到本地的文件名,image-name docker中的镜像名
docker save -o save-file-name.tar image-name 

//将文件导入镜像
docker load --input save-file-name.tar
docker load < save-file-name.tar
```
# Docker 常用命令

##镜像
```shell
#获取镜像
docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]

#列出所有镜像
docker image ls

#构建镜像
docker build -t vmall:v2 .

#运行镜像
docker run -p 8002:8989 vmall:v2

#杀死所有正在运行的容器
docker kill $(docker ps -a -q)

#删除所有已经停止的容器
docker rm $(docker ps -a -q)

#列出虚悬镜像
docker image ls -f dangling=true

#删除虚悬镜像
docker image prune

#删除所有镜像
docker rmi $(docker images -q)
```
##容器
```shell
#启动容器
docker run

#后台运行 -d
docker run -d ubuntu:18.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"

#查看容器
docker container ls

#获取容器输出信息
docker container logs [container ID or NAMES]

#终止容器
docker container stop

#查看终止的容器
docker container ls -a

#删除容器
dicker container rm

#清理所有处于终止状态的容器
docker container prune
```
##进入容器  docker attach 或 docker exec（推荐）

###attach
如果从这个 stdin 中 exit，会导致容器的停止。

```shell
$ docker run -dit ubuntu
243c32535da7d142fb0e6df616a3c3ada0b8ab417937c853a9e1c251f499f550

$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
243c32535da7        ubuntu:latest       "/bin/bash"         18 seconds ago      Up 17 seconds                           nostalgic_hypatia

$ docker attach 243c
root@243c32535da7:/#
```
###exec
当 -i -t 参数一起使用时，则可以看到我们熟悉的 Linux 命令提示符。
如果从这个 stdin 中 exit，不会导致容器的停止。这就是为什么推荐大家使用 docker exec 的原因。
```shell
$ docker run -dit ubuntu
69d137adef7a8a689cbcb059e94da5489d3cddd240ff675c640c8d96e84fe1f6

$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
69d137adef7a        ubuntu:latest       "/bin/bash"         18 seconds ago      Up 17 seconds                           zealous_swirles

$ docker exec -i 69d1 bash
ls
bin
boot
dev
...

$ docker exec -it 69d1 bash
root@69d137adef7a:/#
```
