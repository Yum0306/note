# linux 运维实践
```
1. df -h 查看磁盘占用
2. find / -type f -size +800M  查找磁盘上占用超过800M的文件
3. uname -r 查看linux 的内核版本
4. 添加用户组并添加当前用户到该用户组
sudo groupadd 用户组
sudo gpasswd -a username  用户组
5.清除内存中buff/cache占用 需要在root环境下执行
echo 3> /proc/sys/vm/drop_caches
6.查看指定文件md5值，判断文件是否被修改过
md5sum 文件
```

## 创建定时任务 定时备份docker 容器里面的mysql
#### 1.创建备份脚本
```sh
docker exec -i mysql /bin/bash -c  '/usr/bin/mysqldump -hlocalhost -P3306 -uroot -pwindao2021  --databases eims --comments --compact --lock-tables > /var/lib/mysql/data/databackup/eims.sql'
current=`date "+%Y%m%d%H%M%S"`
mkdir -p /data/mysql/backup/
docker cp mysql:/var/lib/mysql/data/databackup/eims.sql /data/mysql/backup/$current.sql
```
#### 2.创建定时任务执行脚本
```sh
1.添加cron表达式
crontab -e #进入编辑模式
列如:
0 06 * * * ~/backup.sh  
第一个 0代表每个小时的第0分钟
第二个 06代表每天的凌晨6点钟
第三个 * 代表每个月中的任意一天
第四个 * 代表每年中的任意一个月
第五个 * 代表每个星期中的任意一天
注意 第三个位和第五位尽量不要重复
```
## 给服务器设置固定ip
```sh
cd /etc/sysconfig/network-scripts/
vim ifcfg-eno1
内容如下
TYPE="Ethernet"
#MAC地址
HWADDR="a8:5e:45:9f:69:ea"
PROXY_METHOD="none"
BROWSER_ONLY="no"
#static代表固定ip DHCP代表路由器分配
BOOTPROTO="static"
DEFROUTE="yes"
#IP地址
IPADDR=192.168.8.153
#子网掩码
NETMASK=255.255.255.0
#网关
GATEWAY=192.168.10.1
#dns1 
指向路由器ip        
DNS1=192.168.10.1
#dns2指向运营商dns服务器
DNS2=8.8.8.8
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="eno1"
UUID="cd7158bf-97de-4c11-aa53-8119c588a202"
DEVICE="eno1"
ONBOOT="yes"
IPV6_PRIVACY="no"
```
## Centos7+防火墙开放端口
```sh
#开机启动防火墙
systemctl enable firewalld
#开机禁用防火墙
systemctl disable firewalld
#启动防火墙(临时)
systemctl start firewalld
#关闭防火墙(临时)
systemctl stop firewalld
#永久开放80端口
firewall-cmd --zone=public --add-port=80/tcp --permanent  
#重新初始化防火墙 一般新开端口之后要重新初始化 不然可能新开的端口不生效
firewall-cmd --reload
#查看已经开放的端口列表
firewall-cmd --zone=public --list-ports
```
## windows建立共享文件夹，Linux下如何访问
```sh
mkdir share
sudo mount -t cifs -o username=username,password=password //xxx.xxx.xxx.xxx/share ./share
```

## 清理docker占用空间
```shell
docker image prune --all
docker system prune -a
```

## 将指定目录下的所有文件分别打成独立的压缩包
```
ls | xargs -i zip -r {}.zip {}
```

## 免密ssh登录远程主机

#### 1.生成ssh公钥和私钥
```
	ssh-keygen -t rsa -C "你的邮箱地址"
	会在系统用户更目录下.ssh文件夹生成id_rsa(私钥)、id_rsa.pub（公钥）文件
	然后再对应的平台上添加ssh公钥 这个好操作
	然后讲私钥添加到本地ssh管理
	win下需要执行
	1.exec ssh-agent bash
	2.eval ssh-agent -s
	3.ssh-add "id_rsa"
	linux 应该只需要执行3即可
```
#### 2.将公钥传到服务器上
```
	scp ~/.ssh/authorized_keys user@IP:~/.ssh/authorized_keys
```
#### 3.完成上述步骤已经可以进行SSH免密登录了，顺便配置一下 服务器别称
#### 4.打开～/.ssh/config文件，如果没有可以自己创建，按照如下格式添加即可
```
Host 别称名
    Hostname 服务器ip地址
    User 登录用户
    Port ssh登录端口
```
#### 5.测试  ssh 别称名  即可登录

## 查找指定目录下的大文件
```
找出当前目录下 排名前十的占用
du -sh ./* | sort -hr | head
```

##  查找find命令
```
eg: 查找当前指定目录下 所有的target目录 并且删除 -d代表的是 查找目录
find ./ -d -name "target" | xargs rm -rf
```

## SSH + 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzU2MzY5NzcsMTIwNTAyNDI4Miw1MTUwNj
k4Miw1NDUzNjAyNzIsNDY3ODg2OTk5XX0=
-->