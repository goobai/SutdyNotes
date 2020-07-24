
#redis

## redis 安装


```bs
wget http://download.redis.io/releases/redis-5.0.4.tar.gz
tar xzvf redis-5.0.4.tar.gz
cd redis-5.0.4
make
```

##后台运行 
修改redis.config ：~~daemonize no~~
```shell
#daemonize yes 
```

##开启远程访问 
修改redis.config ：~~bind 127.0.0.1~~
```shell

#bind 127.0.0.1
```


##设置密码
```shell
redis-cli
config set requirepass goobai777
```
