# OpenResty实战教程,对文件访问地址进行验证,如果为携带token,或者时间已经过期,则返回401及token无效或者token已过期
## 1.解释一下,啥是OpenResty?
```
刚开始,我以为OpenResty是Nginx的一个模块,后面才了解到,他其实是nginx的一个非官方发行版,是由国内的章亦春大佬编写的,OpenResty其实就是nginx,只是内部集成了大量精良的 Lua 库、第三方模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服务和动态网关。
```
## 2.源码安装Openresty,为了固定版本,多服务下部署下减少版本之间不兼容

```
1.版本: Openresty1.17.8.2、openssl-1.1.1g、pcre-8.44、zlib-1.2.11、gcc相关组件
2.解压后目录
[root@localhost nginx]# ls -l  
total 43804  
drwxr-xr-x. 2 root root 4096 Mar 22 2021 gcc  
-rw-r--r--. 1 root root 27283113 May 30 09:11 gcc.zip  
drwxrwxr-x. 5 admin admin 130 Jul 14 2020 openresty-1.17.8.2  
-rw-r--r--. 1 root root 5041142 May 30 09:08 openresty-1.17.8.2.tar.gz  
drwxrwxr-x. 19 root root 4096 May 29 13:58 openssl-1.1.1g  
-rw-r--r--. 1 root root 9801502 Mar 22 2021 openssl-1.1.1g.tar.gz  
drwxr-xr-x. 9 1169 1169 8192 May 29 13:59 pcre-8.44  
-rw-r--r--. 1 root root 2090750 Mar 22 2021 pcre-8.44.tar.gz  
drwxr-xr-x. 14 501 games 4096 May 29 13:59 zlib-1.2.11  
-rw-r--r--. 1 root root 607698 Mar 22 2021 zlib-1.2.11.tar.gz

3.分别安装
安装gcc相关：
cd gcc && rpm -ivh *.rpm --nodeps --force
yum install gcc-c++ -y
yum install perl -y (这两个涉及的组建比较多,用yum安装比较省心,源码安装需要先安装很多组件)
pcre安装：
cd pcre-8.44/
./configure
make && make install
zlib安装：
cd zlib-1.2.11/
./configure
make && make install
openssl安装：
cd openssl-1.1.1g/
./config
make && make install
4.安装OpenResty
cd openresty-1.17.8.2
./configure \
--prefix=/usr/local/openresty --with-stream --with-luajit --with-http_ssl_module --with-pcre=../pcre-8.  
44 --with-zlib=../zlib-1.2.11 --with-openssl=../openssl-1.1.1g --with-threads --with-http_ssl_module --with  
-http_v2_module --with-http_realip_module --with-http_gzip_static_module --with-http_stub_status_module --build="build at `date +  
%Y-%m-%d`" --with-ld-opt="-Ijemalloc"
gmake && gmake install
```
## 3 编辑nginx.conf配置文件
```
server {  
		listen 8006;  
		lua_code_cache off; #这个设置只是为了开启热部署,你修改了lua脚本会动态加载,重启nginx的时候也会提示,这个会消耗性能,生产中关闭此配置
		#server_name localhost;  
  
		#charset koi8-r;  
		  
		#access_log logs/host.access.log main;  
		location / {  
				charset utf-8;   #这个需要设置字符集,否则返回中文会乱码
				default_type text/html;  
				#content_by_lua_file conf/test.lua;  #是内容处理器，接受请求并输出响应，适用于location、location if。
				access_by_lua_file conf/token.lua;  #在请求访问阶段处理，用于访问控制，适用于http、server、location、location if。
				add_header Access-Control-Allow-Crigin *;  
				add_header Access-Control-Allow-Methods GET,POST,PUT,DELETE,OPTIONS;  
				alias /home/mnt/service/;  
				allow all;  
				autoindex on;  
		}
}
```

## 4.在conf目录下添加token.lua脚本
```
local cjson = require("cjson")			 -- 引入json模块
local uri_args = ngx.req.get_uri_args()  -- 获取请求参数
local uri2 = ngx.var.request_uri		 -- 获取完整请求地址
local timestamp = os.time() * 1000		 -- 获取时间戳
local old_token = uri_args["token"]		 -- 获取参数中的token
local err_token_msg = "token无效!"		 -- token无效提示
local exp_token_msg = "token已经过期!"    -- token过期提示
if old_token == nil then				 -- 未携带token返回401及token无效
    ngx.header['Content-Type'] = 'application/json; charset=utf-8'
    ngx.say(cjson.encode({code = 401,message = err_token_msg}))
    ngx.exit(401)
end
local exp_time = tonumber(uri_args["time"])  -- 获取参数中的过期时间参数
if exp_time == nil then						 -- 时间错误或者
    ngx.header['Content-Type'] = 'application/json; charset=utf-8'
    ngx.say(cjson.encode({code = 401,message = exp_token_msg}))
    ngx.exit(401)
end
local index = string.find(uri2,"&fa")
if index == nil then
    ngx.header['Content-Type'] = 'application/json; charset=utf-8'
    ngx.say(cjson.encode({code = 401,message = err_token_msg}))
    ngx.exit(401)
end
local path = string.sub(uri2,2,(index-1))
local full_path = path .. "_" .."603E0E847391838FB5A12EFE6D6104A3"
local new_sign = string.sub(ngx.md5(full_path),9,24)

if old_token == nil or old_token ~= new_sign then
    ngx.header['Content-Type'] = 'application/json; charset=utf-8'
    ngx.say(cjson.encode({code = 401,message = err_token_msg}))
    ngx.exit(401)
end

if exp_time == nil or timestamp >= exp_time then
    ngx.header['Content-Type'] = 'application/json; charset=utf-8'
    ngx.say(cjson.encode({code = 401,message = exp_token_msg}))
    ngx.exit(401)
end
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODA0MTM3MjcsLTk4MTM4NTM1LDIwNT
AyNTExMzAsMjA3MTc3MjA2XX0=
-->