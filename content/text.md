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


docker run -itd -p 8080:8080 --name platform -e 'SPRING_PROFILES_ACTIVE=pro' -e 'START_PORT=8080' -e 'START_ENV=cloud' -v /home/mnt:/mnt -v /yatai-java/data:/yatai-java/data -v /yatai-java/config:/config --restart=always  docker pull swr.cn-north-1.myhuaweicloud.com/ytwlrj/yatai-school-platform:latest
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEwMDI2ODYzOCw3MjM5MTAyNzcsLTIxMT
IwMzYyNTcsLTE3NDIzNDA1NDQsLTUzOTIzMTkwMSwyMTMyOTgz
NTk1LDExNjk4NjQ4MDAsMTYyMDQzMjM5MCwtMTg3ODA3MjMzNy
wtMjA4ODc0NjYxMl19
-->