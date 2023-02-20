find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;


find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;



find /home/mnt/yatai-java/data/upload/school/ -type d -name -regextype "awk" -regex "(.*[a-zA-Z])" -exec ls -l  
{} \;

find /home/mnt/yatai-java/data/upload/school/ -type d -regextype "awk" -regex "(.*[a-zA-Z])" -exec rm -rf ./{} \;



```
等保会议记录
1.邮件发布管理制度
2.

curl -H "Content-Type: application/json" -H "Access-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJzdWJqZWN0XzE1OTM0MTA4Nz  
MyODcxMTg4NDgiLCJzY2hvb2xJZCI6MTU2OTkxOTM4NjM0NzYzNDY4OCwibmlja25hbWUiOiLlvKDlh68iLCJyb2xlTmFtZSI6IlJPTEVfVEVBQ0hFUiIsInVzZXJUeXBlIjoidGV  
hY2hlciIsImV4cCI6MTY3ODQxMjcxOSwidXNlcklkIjoiMTU5MzQxMDg3MzI4NzExODg0OCIsImlhdCI6MTY3NTgyMDcxOSwidXNlcm5hbWUiOiIxODg2NjY2NjY2NiJ9.n0JpoYB  
yHty5t8_C8J5mhgxpri3VeDVnbFk_3pncskM" -X POST -d '{"pageNo":1,"pageSize":50,"params":{"difficultyCode":"10","knowIdList":["18258288425641  
747499"],"onshelfStateCode":10,"questionKind1Code":1,"sourceFromCode":"CLOUD","subjectId":102}}' "http://127.0.0.1:8082/teacher/v1/prepar  
ation/schQuestion/query" -o output1.txt -s -w time_namelookup:%{time_namelookup}\ntime_connect:%{time_connect}\ntime_starttransfer:%{time  
_starttransfer}\ntime_total:%{time_total}
```

# 

curl -H "Content-Type: application/json" -H "Access-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJzdWJqZWN0XzE1OTM0MTA4Nz  
MyODcxMTg4NDgiLCJzY2hvb2xJZCI6MTU2OTkxOTM4NjM0NzYzNDY4OCwibmlja25hbWUiOiLlvKDlh68iLCJyb2xlTmFtZSI6IlJPTEVfVEVBQ0hFUiIsInVzZXJUeXBlIjoidGV  
hY2hlciIsImV4cCI6MTY3ODQxMjcxOSwidXNlcklkIjoiMTU5MzQxMDg3MzI4NzExODg0OCIsImlhdCI6MTY3NTgyMDcxOSwidXNlcm5hbWUiOiIxODg2NjY2NjY2NiJ9.n0JpoYB  
yHty5t8_C8J5mhgxpri3VeDVnbFk_3pncskM" -X POST -d '{"pageNo":1,"pageSize":50,"params":{"difficultyCode":"10","knowIdList":["18258288425641  
747499"],"onshelfStateCode":10,"questionKind1Code":1,"sourceFromCode":"CLOUD","subjectId":102}}' "http://127.0.0.1:8082/teacher/v1/prepar  
ation/schQuestion/query" -o output1.txt -s -w time_namelookup:%{time_namelookup}\ntime_connect:%{time_connect}\ntime_starttransfer:%{time  
_starttransfer}\ntime_total:%{time_total}

```
1.docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'START_PORT=8080' -e 'SYSTEM_ENV=cloud' -v /mnt2:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always  swr.cn-north-1.myhuaweicloud.com/ytwlrj/yatai-school-platform:latest

2.docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'START_PORT=8080' -e 'SYSTEM_ENV=school' -v /home/mnt:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always  swr.cn-north-1.myhuaweicloud.com/ytwlrj/yatai-school-platform:latest
3.docker pull swr.cn-north-1.myhuaweicloud.com/ytwlrj/yatai-school-platform:latest
```
docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'START_PORT=8080' -e 'SYSTEM_ENV=cloud' -v /home/mnt:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always  swr.cn-north-1.myhuaweicloud.com/ytwlrj/yatai-school-platform:latest

```
学生替换笔记图片
只替换文件
其他端就会有缓存，显示的还是原图
主要是跨设备 a设备已经下载，b设备更新 a设备不知道已经更新
```


```
docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'START_PORT=8080' -e 'SYSTEM_ENV=cloud' -v /mnt2:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always  swr.cn-north-1.myhuaweicloud.com/ytwlrj/yatai-school-platform:10240_1

docker stop platform && docker rm platform && docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'SERVER_PORT=8080' -e 'SYSTEM_ENV=cloud' -v /mnt2:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always  swr.cn-north-1.myhuaweicloud.com/ytwlrj/yatai-school-platform:10240_1

docker run -itd -p 8080:8080 --name platform-temp -e 'SPRING_PROFILES_ACTIVE=pro' -e 'SERVER_PORT=8080' -e 'START_ENV=cloud' -v /home/mnt:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always platform-temp:v1.1


docker stop platform && docker rm platform && docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'SERVER_PORT=8080' -e 'SYSTEM_ENV=cloud' -v /mnt2:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always swr.cn-north-1.myhuaweicloud.com/ytwlrj/platform-temp:1.2
```

```
docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'SERVER_PORT=8080' -e 'START_ENV=cloud' -v /mnt2:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always swr.cn-north-1.myhuaweicloud.com/ytwlrj/platform-temp:1.2
```


```
12170:
docker run -itd -p 8080:8080 --name platform-temp -e 'SPRING_PROFILES_ACTIVE=pro' -e 'SERVER_PORT=8080' -e 'START_ENV=school' -e 'SYSTEM_ENV=school' -v /home/mnt:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always platform-temp:v1.2

prod:
docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'SERVER_PORT=8080' -e 'START_ENV=cloud' -e 'SYSTEM_ENV=school' -v /mnt2:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always swr.cn-north-1.myhuaweicloud.com/ytwlrj/platform-temp:1.2

重庆办：
docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'SERVER_PORT=8080' -e 'START_ENV=school' -e 'SYSTEM_ENV=school' -v /home/mnt:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always  swr.cn-north-1.myhuaweicloud.com/ytwlrj/platform-temp:1.2

景瑞：
docker run -itd -p 8080:8080 --name platform-temp -e 'SPRING_PROFILES_ACTIVE=pro' -e 'START_PORT=8080' -e 'SYSTEM_ENV=school' -v /home/mnt:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always swr.cn-north-1.myhuaweicloud.com/ytwlrj/platform-temp:1.2
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTE5NTEyMzAsMTI4NjY5NjAyMywtNj
g2OTE0MTY0LDE0Mjk2MTg3MDMsLTE0NzAxNTEwMDQsMTMxODAy
ODY2NCwtMTc1Nzg3MDI3NSwxNTY0MTM1MjU3LDIwNDc1OTUwMD
QsMTc1OTI1NDgxNiwxOTgyODk2MTI0LC0xODQxMDEzNDkyLC0x
OTQwNDM0MDM0LC02NTc1OTYxMDQsMjEwMDI2ODYzOCw3MjM5MT
AyNzcsLTIxMTIwMzYyNTcsLTE3NDIzNDA1NDQsLTUzOTIzMTkw
MSwyMTMyOTgzNTk1XX0=
-->