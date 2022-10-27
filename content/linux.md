# linux 运维实践
```
1. df -h 查看磁盘占用
2. find / -type f -size +800M  查找磁盘上占用超过800M的文件
3. find / -type f -size +800M 2>/dev/null | sort -hr | xargs ls -l 查找大于800M的文件并忽略权限不足提示 然后按照从大小到排序，然后在查看列表展示
4. uname -r 查看linux 的内核版本
5. 添加用户组并添加当前用户到该用户组
sudo groupadd 用户组
sudo gpasswd -a username  用户组
5.清除内存中buff/cache占用 需要在root环境下执行
echo 3> /proc/sys/vm/drop_caches
6.查看指定文件md5值，判断文件是否被修改过
md5sum 文件
7.对指定相同后缀名的文件进行批量修改
find ./ -name "*.png" | awk -F "-min.png" '{print $1}' | xargs -i -t mv ./{}-min.png ./{}.png

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

## SSH免密登录 + inotify-tools文件监听 + Docker 实现自动部署
#### 1.SSH配置上面已经有了
#### 2.安装inotify-tools
```
2.1首先安装autoreconf 因为最新版本的inotify-tools 使用autoreconf配置
yum  -y install autoconf automake libtool
2.2去https://codeload.github.com/inotify-tools/inotify-tools/tar.gz/refs/tags/3.22.6.0/inotify-tools-3.22.6.0.tar.gz 下载源文件
2.3 解压 tar -zxvf inotify-tools-3.22.6.0.tar.gz 并进入解压完目录
2.4 执行脚本./autogen.sh 生成configure 配置脚本
2.5 ./configure --prefix=/usr/local/inotify
2.6 make && make install
```
#### 3.添加监听脚本和部署脚本
```
1.监听脚本
#!/bin/sh  
# 监视的文件或目录  
filename=target/yatai-school-platform-1.0-SNAPSHOT.jar  
# 监视发现有增、删、改时执行的脚本  
script=run.sh  
/usr/local/inotify/bin/inotifywait -mq  --format  '%e'  --event close_write $filename | while read event  
do  
	case  $event  in CLOSE_WRITE,CLOSE) bash $script ;;  
	esac  
done

2.打包脚本
docker rm sync -f  
docker rmi sync:v1.0 -f  
docker build -t sync:v1.0 .  
docker run -itd -p 9090:9090 -v /mnt:/mnt -v /xxx-java/data:/xxx-java/data -v /home/sync/config:/config --restart=always --name sync sync:v1.0
```
#### 4.后台静默云监听脚本即可
```
nohup ./monitor.sh &
```

#### baloo
```
1 balooctl suspend // 立即停止
2 balooctl disable // 停用框架
删除index
rm ~/.local/share/baloo/ -rf
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIxMDk5Mzk2MywtODU1NjQ3ODg4LDE0Nz
c1MTkzOTAsLTE1NDg1NjY5ODYsNDgzOTk4ODQwLDEyMDUwMjQy
ODIsNTE1MDY5ODIsNTQ1MzYwMjcyLDQ2Nzg4Njk5OV19
-->