---
title: git pull --rebase实际操作
date: 2024-11-15 18:15:46
tags: Git
---

`git pull --rebase` 命令结合了两个操作：`git fetch` 和 `git rebase`。

`git pull --rebase` 实际上执行了以下操作：
- 从远程仓库拉取最新更新（`git fetch`）
- 将你当前分支（比如 `master`）的提交按序放置在远程分支的最新提交之后（`git rebase`）

这个命令避免了常规的 `git pull` 操作所产生的合并提交。通过使用 `--rebase`，可以将本地提交应用在远程提交的基础上，而不是在一条新的合并提交上。
若这个过程发生了冲突，可以使用 `git rebase --abort` 命令取消正在进行的rebase操作，并且回到rebase操作之前的状态。或者处理了冲突后执行 `git rebase --continue` 继续rebase操作。