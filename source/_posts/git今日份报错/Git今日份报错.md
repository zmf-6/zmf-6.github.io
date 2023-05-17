---
title: Git今日份报错
date: 2021-08-21 10:10:18
tags: ["Git", "fatal"]
---

### 今天在试用 Git 创建项目的时候,在两个分支合并的时候,出现了下面的这个报错.

### 一、fatal:refusing to merge unrelated histories

![image-20210821101640168](https://i.loli.net/2021/08/21/pg6PwtYM219UxIb.png)

### 二、解决方案

在你才做命令后面加上 --allow-unrelated-histories

例如：

```
git merge master --allow-unrelated-histories
```

![image-20210821102012588](https://i.loli.net/2021/08/21/ZrKwghIexNXkJcM.png)

如果你是 git pull 或者 git push 报：fatal:refusing to merge unrelated histories

同理：

```
git pull origin master --allow-unrelated-histories
```
