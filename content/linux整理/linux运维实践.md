## 常用命令
```
1. df -h 查看磁盘占用
2. find / -type f -size +800M  查找磁盘上占用超过800M的文件
3. find / -type f -size +800M 2>/dev/null | sort -hr | xargs ls -l 查找大于800M的文件并忽略权限不足提示 然后按照从大小到排序，然后在查看列表展示
4.对指定目录下超过指定大小的文件名称后缀是指定内容的文件进行置空操作
find /var/lib/docker/containers/ -type f -size +10M -name "*-json.log" -exec truncate -s 0 {} \;
5.对指定相同后缀名的文件进行批量修改
find ./ -name "*.png" | awk -F "-min.png" '{print $1}' | xargs -i -t mv ./{}-min.png ./{}.png
6. uname -r 查看linux 的内核版本
7. 添加用户组并添加当前用户到该用户组
sudo groupadd 用户组
sudo gpasswd -a username  用户组
8.清除内存中buff/cache占用 需要在root环境下执行
echo 3> /proc/sys/vm/drop_caches
9.查看指定文件md5值，判断文件是否被修改过
md5sum 文件
10.删除当前目录下名称叫做target的文件夹
find ./ -d -name "target" | xargs rm -rf
11.找出当前目录下 排名前十的占用
du -sh ./* | sort -hr | head
12.查看当前机器ip 只显示ip
ip addr show|grep -A1 'inet [^f:]'|sed -nr 's#^ +inet ([0-9.]+)/[0-9]+ brd [0-9./]+ scope global .*#\1#p'
10.查看网卡
nmcli connection show
11 如何查看容器使用了哪些进程号
11.1 docker ps  --no-trunc 查看当前容器的长id
11.2 cd /sys/fs/cgroup/memory/docker/容器完整id  去完整目录下
11.3 cat  cgroup.procs
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
DEVICE="eno1"找出当前目录下 排名前十的占用
du -sh ./* | sort -hr | head
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

## baloo
```
1 balooctl suspend // 立即停止
2 balooctl disable // 停用框架
删除index
rm ~/.local/share/baloo/ -rf
```

## 断网监听及重启docker服务脚本,挂上定是任务,即可时刻通过网络状态对服务
```
#!/bin/bash
server="www.baidu.com"
temp=${HOME}/status.temp
container_name=platform
if [ ! -d $temp ];then
    touch $temp
fi
chmod 777 $temp
echo `date "+%Y-%m-%d %H:%M:%S"`
ping $server -W 5 -c 2
if [ $? != 0 ];then
    echo "网络断开了!!"
    echo "NETWORK_CONNECTING=FALSE" > $temp
else
    echo "网络连上了!!"
    result=$(echo `head -n +1 $temp | cut -d= -f 2` | grep "FALSE")
    echo $result
    if [ ! -z $result ];then
        echo "2222网络连上了!!!!"
        docker restart $container_name
    fi
    echo "NETWORK_CONNECTING=TRUE" > $temp
fi
```

## 通过JAVA启动参数配置及docker挂载配置,实现docker内java服务出现爆内存情况时自动重启docker服务

1.在Dockerfile中最后执行jar启动命令上添加 -XX:OnOutOfMemoryError和-XX:OnError 用于当出现OutOfMemory或者Error时执行命令
```
ENTRYPOINT java -XX:OnOutOfMemoryError="docker restart service" -XX:OnError="docker restart service" -jar $JAR_FILE
```
2.在容器启动是挂载docker.sock和docker实现在容器内操作docker
```
docker run -itd -p 8080:8080 --name service -e  -v /var/run/docker.sock:/var/run/docker.sock  -v /usr/bin/docker:/usr/bin/docker   --restart=always  xxxx:latest
```

## Centos内核升级
#### 1.更新yum源仓库  
```  
$ yum -y update  
```  
启用 ELRepo 仓库  
ELRepo 仓库是基于社区的用于企业级 Linux 仓库，提供对 RedHat Enterprise (RHEL) 和 其他基于 RHEL的 Linux 发行版（CentOS、Scientific、Fedora 等）的支持。  
ELRepo 聚焦于和硬件相关的软件包，包括文件系统驱动、显卡驱动、网络驱动、声卡驱动和摄像头驱动等。  
#### 2.导入ELRepo仓库的公共密钥  
```  
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org  
```  
#### 3.安装ELRepo仓库的yum源  
```  
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm  
```  
#### 4.查看可用的系统内核包  
可以看到4.4和4.18两个版本  
```  
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available  
Loaded plugins: fastestmirror  
Loading mirror speeds from cached hostfile  
 * elrepo-kernel: mirrors.tuna.tsinghua.edu.cnelrepo-kernel                                                                                                                                                                 | 2.9 kB  00:00:00     elrepo-kernel/primary_db                                                                                                                                                      | 1.8 MB  00:00:03     Available Packages  
kernel-lt.x86_64                                                                                  4.4.155-1.el7.elrepo                                                                  elrepo-kernel  
kernel-lt-devel.x86_64                                                                            4.4.155-1.el7.elrepo                                                                  elrepo-kernel  
kernel-lt-doc.noarch                                                                              4.4.155-1.el7.elrepo                                                                  elrepo-kernel  
kernel-lt-headers.x86_64                                                                          4.4.155-1.el7.elrepo                                                                  elrepo-kernel  
kernel-lt-tools.x86_64                                                                            4.4.155-1.el7.elrepo                                                                  elrepo-kernel  
kernel-lt-tools-libs.x86_64                                                                       4.4.155-1.el7.elrepo                                                                  elrepo-kernel  
kernel-lt-tools-libs-devel.x86_64                                                                 4.4.155-1.el7.elrepo                                                                  elrepo-kernel  
kernel-ml.x86_64                                                                                  4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
kernel-ml-devel.x86_64                                                                            4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
kernel-ml-doc.noarch                                                                              4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
kernel-ml-headers.x86_64                                                                          4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
kernel-ml-tools.x86_64                                                                            4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
kernel-ml-tools-libs.x86_64                                                                       4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
kernel-ml-tools-libs-devel.x86_64                                                                 4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
perf.x86_64                                                                                       4.18.7-1.el7.elrepo                                                                   elrepo-kernel  
python-perf.x86_64                                                                                4.18.7-1.el7.elrepo                                                                   elrepo-  
```  
#### 5.安装最新版本内核  
```  
$ yum --enablerepo=elrepo-kernel install kernel-ml  
```  
--enablerepo 选项开启 CentOS 系统上的指定仓库。默认开启的是 elrepo，这里用 elrepo-kernel 替换。  
#### 6.设置 grub2  
内核安装好后，需要设置为默认启动选项并重启后才会生效  
查看系统上的所有可用内核：  
```  
$ sudo awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg  
0 : CentOS Linux (4.18.7-1.el7.elrepo.x86_64) 7 (Core)  
1 : CentOS Linux (3.10.0-862.11.6.el7.x86_64) 7 (Core)  
2 : CentOS Linux (3.10.0-514.el7.x86_64) 7 (Core)  
3 : CentOS Linux (0-rescue-063ec330caa04d4baae54c6902c62e54) 7 (Core)  
```  
设置新的内核为grub2的默认版本  
服务器上存在4 个内核，我们要使用 4.18 这个版本，可以通过 grub2-set-default 0 命令或编辑 /etc/default/grub 文件来设置  
方法1、通过 grub2-set-default 0 命令设置  
其中 0 是上面查询出来的可用内核  
```  
grub2-set-default 0  
```  
方法2、编辑 /etc/default/grub 文件  
设置 GRUB_DEFAULT=0，通过上面查询显示的编号为 0 的内核作为默认内核：  
```  
$ vim /etc/default/grub  
GRUB_TIMEOUT=5  
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"  
GRUB_DEFAULT=0  
GRUB_DISABLE_SUBMENU=true  
GRUB_TERMINAL_OUTPUT="console"  
GRUB_CMDLINE_LINUX="crashkernel=auto rd.lvm.lv=cl/root rhgb quiet"  
GRUB_DISABLE_RECOVERY="true"  
```  
生成 grub 配置文件并重启  
```  
$ grub2-mkconfig -o /boot/grub2/grub.cfg  
Generating grub configuration file ...  
Found linux image: /boot/vmlinuz-4.18.7-1.el7.elrepo.x86_64  
Found initrd image: /boot/initramfs-4.18.7-1.el7.elrepo.x86_64.img  
Found linux image: /boot/vmlinuz-3.10.0-862.11.6.el7.x86_64  
Found initrd image: /boot/initramfs-3.10.0-862.11.6.el7.x86_64.img  
Found linux image: /boot/vmlinuz-3.10.0-514.el7.x86_64  
Found initrd image: /boot/initramfs-3.10.0-514.el7.x86_64.img  
Found linux image: /boot/vmlinuz-0-rescue-063ec330caa04d4baae54c6902c62e54  
Found initrd image: /boot/initramfs-0-rescue-063ec330caa04d4baae54c6902c62e54.img  
done  
```  
```  
$ reboot  
```  
#### 7.验证  
```  
$ uname -r  
4.18.7-1.el7.elrepo.x86_64  
```  
#### 8.删除旧内核（可选）  
查看系统中全部的内核：  
```  
$ rpm -qa | grep kernel  
kernel-3.10.0-514.el7.x86_64  
kernel-ml-4.18.7-1.el7.elrepo.x86_64  
kernel-tools-libs-3.10.0-862.11.6.el7.x86_64  
kernel-tools-3.10.0-862.11.6.el7.x86_64  
kernel-3.10.0-862.11.6.el7.x86_64  
```  
方法1、yum remove 删除旧内核的 RPM 包  
```  
$ yum remove kernel-3.10.0-514.el7.x86_64 \  
kernel-tools-libs-3.10.0-862.11.6.el7.x86_64 \  
kernel-tools-3.10.0-862.11.6.el7.x86_64 \  
kernel-3.10.0-862.11.6.el7.x86_64  
```  
方法2、yum-utils 工具  
如果安装的内核不多于 3 个，yum-utils 工具不会删除任何一个。只有在安装的内核大于 3 个时，才会自动删除旧内核。  
安装yum-utils  
```  
$ yum install yum-utils  
```  
删除旧版本　　  
```  
package-cleanup --oldkernels  
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAwNDk0NTQyNywtMjAxMzQ0MzA4OCwyMD
M0ODAxMDcsLTQzMTkzOTA3Ml19
-->