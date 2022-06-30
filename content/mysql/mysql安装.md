windows下
```
1.配置环境变量，将mysql的bin目录配置到环境变量的path变量中
2.在cmd命令行执行 mysqld --install mysql56指令，将mysql数据库服务端注册成windows服务程序
3.启动mysql数据库服务端程序，net start mysql56
4.通过数据库客户端连接数据库服务端 mysql -u root -h 127.0.0.1
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTU2NTk4NDM1LC0yMDgxNDE4MjUxLC04Mj
YyMjIwODBdfQ==
-->