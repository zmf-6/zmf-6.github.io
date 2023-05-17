---
title: blon-online
date: 2021-08-19 10:30:30
tags: ["blon-online"]
---

# 博客怎么上线

1.在 github 中创建一个仓库

```
仓库命名规则：
github用户名.github.io
```

2.找到博客代码目录 3.生成静态资源文件(public)

```
命令：hexo g
```

4.将 public 目录复制到一个新的文件夹里面(需要把 public 里的文件全拿出来)

![image-20210819105359270](https://i.loli.net/2021/08/19/ZgPYpLb8DCB5Ke4.png)

5.在新建文件里初始化 git 并且关联

```
git init  #在目录里面多一个.git文件
git add . #缓存项目
git commit -m "项目描述"
git remote add origin 远程地址
git push origin master
```

6.这时候博客就成功上线啦

```
想要预览的话直接在url里输入
github用户名.github.io
就可以看到你的博客啦
```
