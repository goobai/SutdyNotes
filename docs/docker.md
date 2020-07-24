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
