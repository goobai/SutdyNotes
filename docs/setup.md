

## docker环境安装

```shell script
#安装所需的软件包。yum-utils 提供了 yum-config-manager ，并且 device mapper 
# 存储驱动程序需要 device-mapper-persistent-data 和 lvm2。
yum install -y yum-utils device-mapper-persistent-data lvm2
#设置稳定的仓库。
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
#安装 Docker Engine-Community
yum install docker-ce docker-ce-cli containerd.io
#启动docker
systemctl start docker
```

## 安装项目依赖
```shell script
#安装 mongo rabbitmq elasticsearch
docker pull mongo:latest
docker pull rabbitmq:latest
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.6.2
```

## python环境安装
```shell script

#安装依赖
pyenv 依赖安装
yum -y install gcc gcc-c++ make git patch openssl-devel zlib-devel readline-devel sqlite-devel bzip2-devel
#下载安装脚本
curl https://pyenv.run | bash
#添加环境变量
echo 'export PATH="/root/.pyenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile
#立即生效
source ~/.bash_profile
#查看可以安装的python版本
pyenv install -l
#安装指定python版本
pyenv install 3.6.8
#查看安装的python版本
pyenv versions
#激活某个python版本
pyenv shell 3.6.8
#查看默认安装的插件
ls -la ~/.pyenv/plugins/
#创建python虚拟环境
pyenv virtualenv 3.6.8 env4aipy
#列出python虚拟环境
pyenv virtualenvs
#激活/取消激活python虚拟环境
pyenv activate env4aipy
source deactivate
#虚拟环境的真实目录：~/.pyenv/versions 
#删除虚拟环境
pyenv uninstall my-virtual-env
  #pyenv升级：
cd ~/.pyenv/ 
git pull
```

## docker-compose
```shell script
#安装docker-compose
pip3 install docker-compose

#
docker-compose up
```