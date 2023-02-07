find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;


find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;



find /home/mnt/yatai-java/data/upload/school/ -type d -name -regextype "awk" -regex "(.*[a-zA-Z])" -exec ls -l  
{} \;

find /home/mnt/yatai-java/data/upload/school/ -type d -regextype "awk" -regex "(.*[a-zA-Z])" -exec rm -rf ./{} \;



```
等保会议记录
1.
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUzOTIzMTkwMSwyMTMyOTgzNTk1LDExNj
k4NjQ4MDAsMTYyMDQzMjM5MCwtMTg3ODA3MjMzNywtMjA4ODc0
NjYxMl19
-->