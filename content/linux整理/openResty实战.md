# OpenResty实战教程
## 1.解释一下,啥是OpenResty?
```
刚开始,我以为OpenResty是Nginx的一个模块,后面才了解到,他其实是nginx的一个非官方发行版,是由国内的章亦春大佬编写的,OpenResty其实就是nginx,只是内部集成了大量精良的 Lua 库、第三方模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服务和动态网关。
```
## 2.源码安装Openresty,为了固定版本,多服务下部署下减少版本之间不兼容

```
./configure \
--prefix=/usr/local/openresty --with-stream --with-luajit --with-http_ssl_module --with-pcre=/yatai-java/nginx/pcre-8.  
44 --with-zlib=/yatai-java/nginx/zlib-1.2.11 --with-openssl=/yatai-java/nginx/openssl-1.1.1g --with-threads --with-http_ssl_module --with  
-http_v2_module --with-http_realip_module --with-http_gzip_static_module --with-http_stub_status_module --build="LiveOps build at `date +  
%Y-%m-%d`" --with-ld-opt="-Ijemalloc"
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA1MDI1MTEzMCwyMDcxNzcyMDZdfQ==
-->