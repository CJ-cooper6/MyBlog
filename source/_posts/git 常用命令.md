---
title: git常用命令
date: 2024-11-15 18:15:46
tags: Git
---

```Shell
git branch       查看本地分支
git branch -vv   查看本地分支和远程分支对应关系 
git branch -r    查看远程分支  
git branch -a    查看所有分支  
git branch --set-upstream-to=origin/develop develop 本地关联远程分支
（origin/remote_branch是本地分支对应的远程分支；your_branch你当前的本地分支。）
git branch -d xxx  删除分支，当前分支不能为xxx


git checkout 分支名   切换分支
git checkout -b xxx  以当前分支为基础新建xxx分支（此时push还是push到当前分支的远程分支上，要关联远程分支）
git checkout .       放弃工作区全部修改（未add到暂存区修改的代码）
git checkout -- filename  放弃工作区中某个文件的修改
git checkout -b 新建分支名 目标版本号  基于目标版本创建一个新分支并切换（相比较上面的更安全）

git merge xxx       在当前分支的基础上合并xxx分支上的内容


git fetch              拉取所有远程分支代码   
git fetch origin       拉取origin源上所有分支代码
git fetch origin main  拉取origin源上main分支代码

git remote -v          查看远程仓库信息

git reset --hard 版本号  将分支回退到指定的版本，所有在这个版本之后的commit都删掉了（慎用）
git reset --soft 版本号  会把目标版本之后所有的commit的改动保留在工作区
git reset        取消全部已经使用 git add 添加到暂存区的文件

关联远程分支 
git checkout -b newbranch origin/branch  # 拉取远程分支origin/branch到本地并创建一个新的关联分支
https://blog.csdn.net/Lakers2015/article/details/128388775

git stash 
git stash save "xx"
git stash apply stash@{0} 
git stash clear    删除所有的隐藏更改

git revert     撤销某次提交，用一次新的commit来回滚之前的commit

git branch --contains <commit-hash> 查看某个commit的所有分支

git pull --rebase
git rebase --abort
git cherry-pick <commit-hash>  将某个或多个commit应用到当前分支
```