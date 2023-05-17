---
title: Git教程
date: 2021-08-19 11:13:28
tags: ["Git"]
---

# Git 教程

```
本地删除：git branch -D newBranch  远程删除：git push origin --delete newBranch
```

### 清除本地缓存

```js
git rm -rf --cached .
```

- 查看 git 的版本

```bash
[root@VM-0-9-centos software]# git --version
git version 2.3.0
```

- git add . 添加项目到缓存

- git commit -m '描述' 提交到本地

  <img src="https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/image-20200820154222781.png" alt="image-20200820154222781" style="zoom:50%;" />

- 推送到远程 git push origin 分支的名字(master)

  <img src="https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/image-20200820154347694.png" alt="image-20200820154347694" style="zoom:50%;" />

## 提交到远程

### 提交

1. 不提交 node_modules

<img src="https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/image-20200820154735838.png" alt="image-20200820154735838" style="zoom:50%;" />

2. 初始化 git 仓库

   ```bash
   git init
   ```

3. 提交到缓存

   ```
   git add 某个文件
   git add .
   ```

4. 提交到本地

   ```bash
   git commit -m 描述
   git commit -m '人生第一次'
   ```

5. 查看是否关联远程地址

   ```bash
   git remote -v
   ```

6. 关联远程仓库地址远程

   <img src="https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/image-20200820155506882.png" alt="image-20200820155506882" style="zoom:50%;" />

   ```bash
   git remote add origin 远程的地址
   git remote add origin https://gitee.com/bingyu123/server.git
   ```

7. 提交到远程

   ```bash
   git push origin 分支的名字
   git push origin master
   ```

   <img src="https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/image-20200820155651023.png" alt="image-20200820155651023" style="zoom:50%;" />

## 拉

- 在服务器拉取
- /opt/project 中拉取
- cd /opt/project

- 克隆 git clone 地址

  <img src="https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/image-20200820165727777.png" alt="image-20200820165727777" style="zoom:50%;" />

- cd /server && npm i 下载依赖

- node index.js 启动项目

- 从远程拉取最新文件

  ```bash
  git pull origin 分支
  git pull origin master
  ```

  <img src="https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/image-20200820171043714.png" alt="image-20200820171043714" style="zoom:50%;" />

- 启动服务器 node index.js

## vue/react 开发的前端 后台 : express 服务器

- 开发环境 : npm run dev 200M
- 前端的项目打包 1-10 M
- 将前端打包之后的文件放到 什么文件夹中 public

#### git 基础命令

```javascript
git init //初始化
git rm -r --cached .(可能没有点) //清空缓存
dir //查看文件信息
git add . ||git add 文件名 //本地文件提交到本地仓库
git commit -m "随意名称（已修改）"
git push -u origin master (-f)//第一次推送远程分支,-f代表强制提交，替换远程分支整体内容

git status //查看提交状态
git remote //查看链接是否成功
git clone  //远程仓库地址

git checkout -b 分支名称 //创建并切换分支
git checkout 分支名称  //切换分支
git branch -d 分支名 //删除分支
git branch //查看在哪个分支下
git branch -a //查看本地全部分支
git branch -al //查看本地于远程分支

git push origin --delete 名称  //删除远程分支于追踪分支，（本地于远程分支建立的并联关系）
```

#### git 直接拉取远程仓库分支到本地

```javascript
git init //初始化
git remote add origin 远程仓库地址 //关联远程仓库
git fetch origin develop //拉取指定远程分支到本地
// develop为远程仓库分支名

git checkout -b szy origin/szy //本地创建分支并切换到该分支//跟踪远程分支
```

#### git 将本地项目提交到远程分支上（git 上）

```javascript
//项目已拉取过
git add .
git commit -m  //"注释"（添加注释 可选）
git push origin master //(分支名) 提交到远程仓库
//项目未拉取过
git init
git remote add origin 远程仓库地址 //关联远程仓库
//如果(出现origin exitss  输入git  remote  rm  origin，再次执行上面那条语句)
git pull origin master
 git add .
 git commit -m "注释"（添加注释 可选）
 git push origin master
```

```js
 如果提交git push origin master，出现failed to push some refs to git回想一下，创建该项目时显示尝试使用了git for win的客户端离线版，发现不能上传，又在github上重新创建仓库，建立README.md，导致该文件不在本地代码中

可以通过以下方式解决

git pull --rebase origin master

执行后可以看到本地代码中多了README.md文件

再次执行git push origin master即可完成代码上传
```

#### git 远程仓库被修改后，本地仓库提交出错（任何解决冲突问题）

```javascript
//报错问题
 ! [rejected]        master -> master (non-fast-forward)
//解决方案
git init //初始化
git remote add origin 远程仓库地址 //关联远程仓库
git fetch origin develop //拉取指定远程分支到本地
// develop为远程仓库分支名

git checkout -b dev origin/develop //本地创建分支并切换到该分支

//先拉取远程仓库之后，需要再次提交直到出现报错（如直接执行
//git pull origin wp --allow-unrelated-histories 则会将原本地代码冲突地方覆盖），执行下方操作
git pull origin master --allow-unrelated-histories
git add .
git commit -m "已修改"
git push origin master
//上传成功

方法二：强推
即利用强覆盖方式用你本地的代码替代git仓库内的内容
git push -f origin master

方法三：
先把git的东西fetch到你本地然后merge后再push
//拉取远程到本地20[7]
git fetch
git merge
```

-
