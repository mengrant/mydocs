## Git命令

| 命令 | 说明 |
| --- | --- |
|  git init   | 在一个目录中执行，将此目录初始化为git管理仓库 |   
| git checkout -- readme.txt | 把readme.txt文件在工作区的修改全部撤销，这里有两种情况：一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次git commit或git add时的状态。|
| git rm filename | 从版本库中删除一个文件 ，需要用git commit提交到版本库 |
| git clone gitsorce | 在当前目录下，获取一分git资源的克 |
| git remote add origin git@server-name:path/repo-name.git | 关联一个远程库 | 
| git push -u origin master | 远程仓库如果没有内容，第一次提交时，加-u参数，将本地的master分支与远程的合并，此后提交就不需要加-u参数了 |
| git push origin master | 把本地仓库推送到远程仓库 |
| git checkout -b \<name> | 创建 并切换分支 |
| git branch | 查看当前分支 |
| git branch \<name> | 创建分支 |
| git checkout \<name> | 切换分支 | 
| git merge \<name> | 合并指定分支到当前分支 |
| git branch -d \<name> | 删除指定的分支 |
