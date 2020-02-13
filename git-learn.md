
学习网址：https://www.liaoxuefeng.com/wiki/896043488029600

* git学习对git有了相对系统的认识，将常用命令进行梳理总结
<br>如何在本地创建一个git库并与远程仓库联系起来？
<br>如何同时绑定多个远程仓库？
<br>查看日志，版本回退
<br>分支管理等

### git常用命令，参见git-changset.pdf
1. git diff: 查看修改的文件内容
2. **git reflog: 记录每次执行的git命令**
3. git log: 查看提交历史

4. 撤销修改
   * 如果在本地(工作区)：
     **git  checkout --file_name: 
       撤销工作区的修改，即恢复被删除的文件
       如果没有--，表示切换分支**
   * 如果已经commit(暂存区)：
       1. git reset HEAD file_name: 把暂存区的修改撤销，版本回退的前提是没有提交到远程仓库，
       2. 然后再git checkout --file_name

5. 删除文件
   * rm file_name 删除本地文件
   * git rm file_name 删除版本库中的文件，并且git commit
   * 删除远程仓库中的文件
     1. rm file_name
     2. git commit -m "remove file_name"
     3. git push origin master
   * 删除远程仓库？？？？？？
   
6. 本地初始化git仓库，添加到远程仓库：
    git remote add origin git@github.com:michaelliao/learngit.git
    * git remote rm origin 删除本地仓库与远程的连接
    * git push -u: 因为远程仓库为空，第一次push必须要添加-u

7. 分支管理
    * git branch name创建分支
    * git checkout name 切换分支
    * git checkout -b name  或git switch -c name 创建并切换分支
    * git branch 查看分支，前面带*表示当前分支
    * git merge 合并分支
    * git branch -d name 删除分支
    * git brach -D name 强行删除分支
    * git merge发生冲突后，查看冲突文件，并修改对应的内容
    * git log --graph 显示分支合并图
    * git log --pretty=oneline --abbrev-commit 更清晰显示图

8. 实际工作中一般不会在master分支工作，设置分支，在分支上进行工作，然后合并
    * 修复bug时通常重新建立分支，再分支上修复后再合并，然后删除bug分支
    * git pull 拉取远程仓库的代码，强制覆盖本地的代码，
      防止本地修改丢失，应该使用git stash保存本地的修改
    * git stash 缓存未完成的工作
    * git stash list 查看缓存的内容
    * git stash pop 恢复未完成的内容，并删除stash
    * 如果master分支有bug, 其余分支也有相同的bug, 可以利用git cherry-pick id 进行修复，id是指commit的id
      远程仓库的默认名字origin
    * git push origin master 把本地分支的所有内容推送到远程分支
      查看远程库信息，使用git remote -v；

9. 本地新建的分支如果不推送到远程，对其他人就是不可见的；
    * 从本地推送分支，使用git push origin branch-name，
    * 如果推送失败，先用git pull origin master抓取远程的新提交；
    * 在本地创建和远程分支对应的分支 git checkout -b branch-name origin/branch-name，
      本地和远程分支的名称最好一致；
    * git pull 失败后提示，可以建立本地分支和远程分支的关联 git branch --set-upstream branch-name origin/branch-name
    * 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
    * git rebase 使分支提交历史成为一条直线，更加清晰

10. 标签，id一般较长，将版本号与id绑在一起更方便
    * git tag name commit_id 创建版本号
    * git tag -a name -m 描述信息 commit_id 添加描述信息
    * git show name 展示绑定的commit_id信息
    * git log 查看标签列表
    * 删除标签 git tag -d name
      <br>上传到远程仓库 git push origin name
      <br>全部上传 git push origin --tags
      <br>如果上传到远程，需要先删除本地，再删除远程的，删除
      远程的代码 git push origin :refs/tags/tagname

11. 本地仓库可以同时关联多个远程分支
    * git init 初始化本地目录为git仓库
    * git remote add github git@github.com/chen_liu_123/learngit.git 
    * git remote add origin  http://gitee.com/chen_liu_123/learngit.git 
    * git push github master
    * git push origin master

12. 配置git
    * 给命令设置别名 git config --global alias.ci commit
    * global表示为所有的仓库执行相同的命令
    