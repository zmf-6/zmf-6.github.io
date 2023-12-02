---
title: Git使用规范
date: 2023-12-02 12:25:18
tags: ["Git", "rebase"]
---

## 第一步 新建分支

获取主干最新代码

```
git checkout dev
git pull
```

新建一个开发分支 myFeature，使用jira任务号

```
git checkout -b myFeature
例如：task/XMSJSWH-191
```

## 第二步 提交分支commit

分支修改后，就可以提交commit了

```
git status 查看修改了那些内容
git add --all 或者 git add . 或者 git add 文件 
git status 查看是否已将要提交的内容进行了添加
git cz 对此次提交添加描述，具体参照commit提交规范
```

注意

- `git add`命令的all参数，表示保存所有变化（包括新建、修改和删除）。从git 2.0开始，all 是`git add` 的默认参数，所以也可以使用`git add .` 代替。如果只是提交部分文件，不要使用all。
- `git status` 命令，是用来查看发生变化的文件

提交commit后提交到远端分支并提交code review。

## 第三步 合并commit

分支开发完成后，有可能有一堆commit，但是合并到这主干的时候，往往希望只有一个（或最多三个）commit，这样不仅清晰，也容易理解。

```
git rebase -i commitid
```

```
pick 7e738f7d1 fix() 处理client层弃用代码
pick 96a9f34ef fix() 处理client层弃用代码
pick 7d9b3e8d1 fix() 处理模块依赖问题
pick b18c9cc02 fix:重构依赖问题
pick ff46e71b7 fix:重构依赖问题
pick 6f502d9ff fix() client重名
pick 26d898506 fix() client重名
pick 19b99bb09 fix(OUTBOUND) :修复manage依赖 close :dev-new3

# Rebase cbca11365..19b99bb09 onto cbca11365 (8 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was

# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
#	If you remove a line here THAT COMMIT WILL BE LOST.
#
#       However, if you remove everything, the rebase will be aborted.
#
#
# Note that empty commits are commented out
~                                  


```



- pick：保留该commit（缩写:p）

- reword：保留该commit，并且修改提交信息（缩写:r）

- edit：保留该commit, rebase时会暂停，允许你修改这个commit（缩写:e）

- squash：将该commit和前一个commit合并（缩写:s）

- fixup：将该commit和前一个commit合并，但不会保存当前的commit说明信息（缩写:f）

- exec：执行其他shell命令（缩写:x）

- drop：丢弃当前commit（缩写:d）

  

上面命令中，squash和fixup可以用来合并commit。先需要把合并的commit前面的动词，改为squash（s）或者fixup（f）。

```
pick 7e738f7d1 fix() 处理client层弃用代码
s 96a9f34ef fix() 处理client层弃用代码    
f 7d9b3e8d1 fix() 处理模块依赖问题   
s b18c9cc02 fix:重构依赖问题   
f ff46e71b7 fix:重构依赖问题   
s 6f502d9ff fix() client重名   
f 26d898506 fix() client重名   
s 19b99bb09 fix(OUTBOUND) :修复manage依赖 close :dev-new3
```

运行结果会生成一个commit，但会有5个commit的说明信息。

合并commit之后，要在自测一遍。

## 第四步 与主干同步

```
git fetch origin
git rebase origin/dev 
```

解决冲突原则：后提交代码的人解决冲突，保证质量。



## 第五步 推送到远程仓库

```
git push origin myFeature:dev
```



## 其他

- 保持代码干净整洁，符合证通代码规范

- 不需要的代码直接删除，然后提交到git。以后恢复使用git revert命令恢复。

- 回退整个commit，使用git revert，不要手工删代码。

- 开发工程中的代码可提交到远端仓库，防止代码丢失，开发完成后合并commit。

  - 个人开发branch可提交到个人分支远端，保证主分支整洁；

- 本地代码修改了一半，需要切换到其他分支

  - 方案一：`git stash`; `git checkout newbranch`. 切回后执行`git stash pop`
  - 方案二：`git add .` ; `git commit `; `git checkout new branch`

- 本地代码修改了一半，放弃丢改修改

  - `git checkout file` 放弃file的修改
  - `git checkout -f`  放弃所有文件
  - `git clean -xdf . `清楚所有新增文件

- 本地代码修改了一半，保存到一个新建的临时分支上

  - `git checkout -b newbranch`

  - `git add . `

  - `git commit `

    