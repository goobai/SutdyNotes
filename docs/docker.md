# docker


## docker修改镜像

将文件/etc/docker/daemon.json修改为一下内容：
```shell script
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}

```
重启docker
```shell script
systemctl restart docker
```