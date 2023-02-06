find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;


find /home/mnt -type d -regextype "awk" -regex "[a-zA-Z]" -exec truncate -s 0 {} \;



find /home/mnt/yatai-java/data/upload/school/ -type d -name -regextype "awk" -regex "(.*[a-zA-Z])" -exec ls -l  
{} \;
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE2OTg2NDgwMCwxNjIwNDMyMzkwLC0xOD
c4MDcyMzM3LC0yMDg4NzQ2NjEyXX0=
-->