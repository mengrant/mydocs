# Git命令

| 命令 | 说明 |
| --- | --- |
|  git init   | 在一个目录中执行，将此目录初始化为git管理仓库 |   
| git checkout -- readme.txt | 把readme.txt文件在工作区的修改全部撤销，这里有两种情况：一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次git commit或git add时的状态。|
| git rm filename | 从版本库中删除一个文件 ，需要用git commit提交到版本库 |
| git clone gitsorce | 在当前目录下，获取一分git资源的克 |
