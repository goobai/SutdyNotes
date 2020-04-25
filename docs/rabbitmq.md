# RabbitMq集群配置


## 将多个节点组成rabbitmq集群
1、配置各个结点host文件(/etc/hosts)
```shell script
192.18.0.2 node1
192.18.0.3 node2
192.18.0.4 node3
``` 
2、设置各节点的cookie(/var/lib/rabbitmq/.erlang.cookie)

3、配置集群。
```shell script

rabbitmqctl cluster_status
#1.启动rabbitmq
rabbitmq-server -detached
#2.依次将2、3节点加入集群
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl join_cluster rabbit@node1
rabbitmqctl start_app

```
## 从集群中删除某个节点  