## git配置
```  
ssh-keygen -t rsa -C "i@vim.plus"  
会在系统用户更目录下.ssh文件夹生成id_rsa(私钥)、id_rsa.pub（公钥）文件  
然后再对应的平台上添加ssh公钥  这个好操作  
然后讲私钥添加到本地ssh管理  
win下需要执行  
1.exec ssh-agent bash  
2.eval ssh-agent -s  
3.ssh-add "id_rsa"  
linux 应该只需要执行3即可  
然后再正常执行 git init add 等操作  
```  
##  .gitignore  
```  
HELP.md  
target/  
!.mvn/wrapper/maven-wrapper.jar  
!**/src/main/**/target/  
!**/src/test/**/target/  
!**/logs/  
*.log  
  
### STS ###  
.apt_generated  
.classpath  
.factorypath  
.project  
.settings  
.springBeans  
.sts4-cache  
  
### IntelliJ IDEA ###  
.idea  
*.iws  
*.iml  
*.ipr  
  
### NetBeans ###  
/nbproject/private/  
/nbbuild/  
/dist/  
/nbdist/  
/.nb-gradle/  
build/  
!**/src/main/**/build/  
!**/src/test/**/build/  
  
### VS Code ###  
.vscode/  
  
```  
## git ssh 非22端口  
```  
ssh -T -p222 git@127.0.0.1 可以测试配置git ssh免密之后是否生效  
git remote add origin ssh://git@127.0.0.1:222/java/test.git  
```


## git常用命令
```
git config --global user.name "qyc"   //初始化本地的git用户名 和远程的帐户名和密码无关 只是让其他开发协作者能知道是谁提交的
git config --global user.email "i@vim.plus"  //初始化本地git的邮箱
git config --system --unset credential.helper //清除本地保存的git 用户名和密码


git init  在项目根目录下初始化本地git 仓库
git add dir/file/.  添加文件夹或者目录或者全部东西 到本地仓库
git commit -m "msg"  添加提交备注
git remote add localRemotename path  将本地仓库和远程仓库地址进行连接 localRemotename一般为origin path 指向远程仓库 ，remote可以添加多个
git remote remove localRemotename  将本地保存的远程仓库地址删除
git push origin master 将本地代码推送到 远程origin地址 的master分支
git pull origin master 将远程地址origin的master分支拉去到本地
git checkout -b newBranchName  在本地新建一个分支并切换
git branch -d branchName  将本地的制定分支删除
git checkout branchName  切换到指定的本地分支
git clone path 克隆远程代码到本地

假设原来在xxx分支 代码合并到master分支
git checkout master
git merge xxx 这样 xxx分支就合并到本地master分支了

git reset --hard origin/master  会滚本地代码到origin/master 分支的最新提交记录

经常会忘记添加.gitignore 文件
git rm -rf --cached dir/file/.   删除本地缓存记录
git log 查看提交记录
git status 查看本地文件状态


windows /linux 下配置ssh密钥 免密登录
win下 右键单击打开 git bash
ssh-keygen -t rsa -C "i@vim.plus"
会在系统用户更目录下.ssh文件夹生成id_rsa(私钥)、id_rsa.pub（公钥）文件
然后再对应的平台上添加ssh公钥  这个好操作
然后讲私钥添加到本地ssh管理
win下需要执行
去到你的用户根目录
1.exec ssh-agent bash
2.eval ssh-agent -s
3.ssh-add id_rsa
linux 应该只需要执行3即可
然后再正常执行 git init add 等操作


```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxNDQ1ODEwOF19
-->