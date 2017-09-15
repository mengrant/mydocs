## Git命令
<style>
table th:first-of-type {
    width: 220px;
}
</style>

| 命令 | 说明 |
| --- | --- |
|  git init   | 在一个目录中执行，将此目录初始化为git管理仓库 |   
| git add \<name> | 添加文件到git管理器中 |
| git commit | 提交到本地库 |
| git commit -m "blabla..." |提交时添加说明 |
| git status | 查看当前git工作区状 |
| git checkout -- readme.txt | 把readme.txt文件在工作区的修改全部撤销，这里有两种情况：一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次git commit或git add时的状态。|
| git reset --hard \<commitId> | 回退到指定版本 |
| git reset HEAD <file> | 把暂存区的修改撤销掉 |
| git rm \<name> | 从版本库中删除一个文件 ，需要用git commit提交到版本库 |
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
| git log --graph | 可以查看分支合并图|
| git log --graph --pretty=oneline --abbrev-commit | |
| git merge --no-ff -m "nerge with no fast forward" \<name> | 强制使用no fast forward模式合并项目|
| git stash | 保存当前的工作内容到工作区 |
| git stash list | 显示工作区保存的工作内容的列表 |
| git stash apply | 恢复工作区内容  到工作现场，但是工作区内容不会删除 |
| git stash drop | 删除工作区内容 |
| git stash pop | 从工作区恢复内容到工作现场，并删除工作区内容 |
| git branch -D \<name> | 强行删除一个没有被合并的分支 |
| git remote | 查看远程库的信息 |
| git remote -v | 查看远程库的详细信息，可能查看fetch和push的地址 |
| gir remote rm \<name> | 删除一个远程连接 |
| git push origin master| 将本地主库推送到远程库|
| git push origin dev | 将本地分支库推送到远程库 |
| git checkout -b dev origin/dev | 创建本地分支并与远程分支关联|
| git pull | 拉取远程信息到本地   `如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令 git branch --set-upstream branch-name origin/branch-name。` |
| git tag \<tagname> | 给当前commit打标签 |
| git tag -a \<tagname> -m "blabla..."  [commitId] |指定标签名称和标签信息 |
| git tag -s \<tagname> -m "blabla..."  [commitId] |用PGP签名标签 |
| git tag | 查看所有标签 |
| git tag -d \<tagname> |删除标签|
| git push origin \<tagname>| 推送标签到远程库 |
| git push origin --tags | 推送全部未推送过的本地标签|
| git tag -d \<tagname> | 删除一个本地标签 |
| git push origin :ref/tags/\<tagname> | 删除一个远程标签 |
| git remote rm origin | 删除与远程库的关联 |
| git add -f \<name> | 强制添加一个被忽略的文件 |
| git check-ignore | 检查忽略文件 |
| git config --global alias.st status   <br/>  git config --global alias.co checkout  <br>git config --global alias.ci commit  <br> git config --global alias.br branch <br> git config --global alias.unstage 'reset HEAD'| 设置git 命令别名|
| git config --global alias.last 'log -1' | 用git last 显示最后一次提交 |
| git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit" | git lg  显示全部信息 |
