# OpenResty实战教程
## 1.解释一下,啥是OpenResty?
```
刚开始,我以为OpenResty是Nginx的一个模块,后面才了解到,他其实是nginx的一个非官方发行版,是由国内的章亦春大佬编写的,OpenResty其实就是nginx,只是内部集成了大量精良的 Lua 库、第三方模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服务和动态网关。
```
## 2.源码安装Openresty,为了固定版本,多服务下部署下减少版本之间不兼容

```
1.版本: Openresty1.17.8.2、openssl-1.1.1g、pcre-8.44、zlib-1.2.11
2.解压后目录
[root@localhost nginx]# ls -l  
total 17156  
drwxrwxr-x. 5 admin admin 130 Jul 14 2020 openresty-1.17.8.2  
-rw-r--r--. 1 root root 5041142 May 30 09:08 openresty-1.17.8.2.tar.gz  
drwxrwxr-x. 19 root root 4096 May 29 13:58 openssl-1.1.1g  
-rw-r--r--. 1 root root 9801502 Mar 22 2021 openssl-1.1.1g.tar.gz  
drwxr-xr-x. 9 1169 1169 8192 May 29 13:59 pcre-8.44  
-rw-r--r--. 1 root root 2090750 Mar 22 2021 pcre-8.44.tar.gz  
drwxr-xr-x. 14 501 games 4096 May 29 13:59 zlib-1.2.11  
-rw-r--r--. 1 root root 607698 Mar 22 2021 zlib-1.2.11.tar.gz
3.分别安装
unzip gcc.zip
cd gcc && rpm -ivh *.rpm --nodeps --force
yum install gcc-c++ -y
yum install perl -y
进入nginx目录
unzip nginx.zip
pcre安装
执行如下命令：
tar -zxvf pcre-8.44.tar.gz
cd pcre-8.44/
./configure
make && make install
zlib安装
执行如下命令：
tar -zxvf zlib-1.2.11.tar.gz
cd zlib-1.2.11/
./configure
make && make install
openssl安装
执行如下命令：
tar -zxvf openssl-1.1.1g.tar.gz
cd openssl-1.1.1g/
./config
make && make install


./configure \
--prefix=/usr/local/openresty --with-stream --with-luajit --with-http_ssl_module --with-pcre=/yatai-java/nginx/pcre-8.  
44 --with-zlib=/yatai-java/nginx/zlib-1.2.11 --with-openssl=/yatai-java/nginx/openssl-1.1.1g --with-threads --with-http_ssl_module --with  
-http_v2_module --with-http_realip_module --with-http_gzip_static_module --with-http_stub_status_module --build="LiveOps build at `date +  
%Y-%m-%d`" --with-ld-opt="-Ijemalloc"
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc1NjMzODEzMiwyMDUwMjUxMTMwLDIwNz
E3NzIwNl19
-->