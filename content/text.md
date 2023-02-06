find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;


find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;



find /home/mnt/yatai-java/data/upload/school/ -type d -name -regextype "awk" -regex "(.*[a-zA-Z])" -exec ls -l  
{} \;

find /home/mnt/yatai-java/data/upload/school/ -type d -regextype "awk" -regex "(.*[a-zA-Z])" -exec rm -rf ./{} \;
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEzMjk4MzU5NSwxMTY5ODY0ODAwLDE2Mj
A0MzIzOTAsLTE4NzgwNzIzMzcsLTIwODg3NDY2MTJdfQ==
-->