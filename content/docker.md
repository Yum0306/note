# 1.常用命令
#### **1.安装之后启动docker**
~~~
systemctl start docker
~~~
#### **2.docker添加镜像**
~~~
docker pull xxxx镜像
例如:有点坑的rabbitmq（带有web管理界面的rabbitmq）
docker pull rabbitmq:3.7.7-management
~~~
#### **3. docker 运行镜像**
~~~
docker run -d -p 端口号（-p 端口号 可以多个） 镜像名
docker run -d -p 端口号
~~~
#### **4.docker 结束掉运行的镜像**
~~~
docker stop 镜像CONTAINER ID
~~~
CONTANER ID 可通过docker ps 查看正在运行的镜像
#### **5.查看正在运行的镜像**
~~~
docker ps
~~~
查看所有的镜像 之前运行过的
~~~
docker ps -a
~~~
#### **6.移除仓库里面的镜像文件**
~~~
docker rmi -f  镜像IMAGE ID
~~~
IMAGE ID可通过docker images 查看仓库中已存在的镜像
#### **7.查看仓库中已存在的镜像**
~~~
docker images
~~~
### **8.镜像的启动与停止**
~~~
docker start [CONTAINER ID]
docker stop [CONTAINER ID]
~~~
### **9.进入镜像**
~~~
docker exec -it [CONTAINER ID] 路径
eg：
docker exec -it 60dd60d9ea5a bash (centos)
~~~
# 2.常用工具端口
## 2.1.redis 6379
## 2.2 mongoDB 
~~~
27017     mongod 和 mongos 实例的默认端口。你可以通过 port 或 --port 改变该端口。
27018     设置 --shardsvr 运行变量或在配置文件里设置 clusterRole 为 shardsvr 时的默认端口。
27019     设置 --configsvr 运行变量或在配置文件中将 clusterRole 设置为 configsvr 时的默认端口。
28017     系统状态网页的默认端口。系统状态网络页面永远可以在比 port 大 1000 的端口反问。
~~~
## 2.3.rabbitMQ
~~~
4369     erlang发现口
5672     client端通信口
15672    管理界面ui端口
25672    server间内部通信口
~~~

### 2.4docker自动操作防火墙开放端口
~~~
默认情况下, docker启动后参数中如果加了端口映射, 就会自动将端口开放给所有网络设备访问,  
并且这种情况下即使在本机的系统防火墙中加规则也无效, 因为docker会自动添加一个优先级最高的针对这个映射端口全开放规则,  
这样就需要在docker启动时添加参数来禁止docker对本机防火墙的操作.
~~~
docker


### 在docker容器中使用clear命令失败解决方法
```
dnf install ncurses -y
以下不是
dnf install libaio -y  
dnf install numactl -y
```

### docker启动失败 查看失败原因
```
dockerd --debug
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzM1ODEzMzAyLDE2MTQ2MTY5MTgsODEyMz
czMzc0LC0zNDU3NDcyMDZdfQ==
-->