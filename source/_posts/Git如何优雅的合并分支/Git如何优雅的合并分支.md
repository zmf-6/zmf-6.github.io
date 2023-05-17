---
title: Git如何优雅的合并分支
date: 2021-08-22 20:22:28
tags: ["Git"]
---

# Git 如何优雅的合并分支

在项目中，我们总会创建很多分支进行不同功能或者需求的开发，等功能完成后再合并回主分支。那么如何才能优雅的合并分支呢？如果此时你提起了兴趣，那么不妨继续读下去了。

## 建立多人开发场景

### 1. 创建仓库

```
// 初始化仓库
git init
// 创建a.txt
touch a.txt
// 创建b.txt
touch b.txt
// 加入暂存区
git add .
// 提交
git  commit -m 'initial'
```

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/232ecd0b900e4a83beec4552196e41c7~tplv-k3u1fbpfcp-watermark.awebp)

### 2. 创建 feature 分支

```
git checkout -b feature
```

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/20604cb6023d48fdaf93f9ce129a4ac7~tplv-k3u1fbpfcp-watermark.awebp)

### 3. 两个分支同时开发

feature 分支开发下一版本新功能，提交了两次，分别修改 a.txt 文件和 b.txt 文件。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7098ad37c30240eeb171ac020f1417c3~tplv-k3u1fbpfcp-watermark.awebp)

master 分支开发本次版本功能，同样提交了两次，且修改了 a.txt 文件和 b.txt 文件。

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9f0e58c575b4578b94f3f876ef8f35e~tplv-k3u1fbpfcp-watermark.awebp)

当前分支情况如下图，各节点上面的字符是每次 commit 的散列值，当前 master 分支的 header 在 c5 节点上，feature 分支的 header 在 c3 节点上。

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/482f38e4c01b43b48d5ab7d45b1c3cd2~tplv-k3u1fbpfcp-watermark.awebp)

这个时候需要将 feature 分支合并回 master 分支，有两种方案：

1. 在 master 分支上直接 merge feature 分支；
2. 是先在 feature 分支上 rebase(变基)，然后在 master 分支上 merge feature 分支。

下面分别说明一下这两种方式：

## git merge

git merge 操作比较暴力，也是用的比较多的方式，下面演示的是 feature 分支合并至 master 分支，具体过程如下：

1. 找到 feature 分支和 master 分支的最近共同祖先 commit 节点 c1；
2. 把 feature 分支的最新一次 commit 节点 c3 和 master 分支上的最新一次 commit 节点 c5 合并，此时若有冲突，则一次性解决所有冲突，然后生成一个新的 commit 节点 c6；
3. 同时根据两个分支上的 commit 时间的先后顺序，依次放到 master 分支上，使用 git log 可以看到时间顺序。

上面流程的结果示意图如下所示：

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d893f22b0f9e49b1a717fe38c3da4824~tplv-k3u1fbpfcp-watermark.awebp)

在项目中的操作命令如下。可以看到执行 `git merge feature` 命令后，存在冲突，进入 merging 工作区，然后一次性解决所有冲突后，提交一个新的 commit。

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f05139d6da8b43d1bdb68586c8bd4a68~tplv-k3u1fbpfcp-watermark.awebp)

执行 gitk 命令行，可以在界面上看到当前分支如下图所示。有一个新的 commit。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/02bbc6fe7c67442a8ebaa363a1eae74f~tplv-k3u1fbpfcp-watermark.awebp)

## git rebase

这个命令从名字上就可以直观看出它的功能：改变当前的分支的`基点`。对于 feature 分支，它是从 master 分支的 c1 节点创建的分支，所以它的`基点`就是 c1。如果在 feature 分支上执行 git rebase master ，其过程大致如

1. 找到当前 master 分支最新的 commit 节点 c5，将 feature 分支的基点变成 c5 节点。；
2. 若 feature 分支与 master 分支存在冲突，那么将根据 feature 分支的提交时间，依次解决冲突，并修改 feature 分支此次 commit 的散列值。
3. 最终在分支上看，呈现一条直线，但是存在历史 commit 覆写的问题。

上面过程的结果示意图如下所示，其中 c2'和 c3'表示散列值改变了。

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e63ef15bb331464f990c987ecaa934be~tplv-k3u1fbpfcp-watermark.awebp)

> 值得注意的是，执行 rebase 操作的时候，需要保证 master 分支处于最新状态，否则在 merge 合并的时候也可能存在冲突，就失去使用 rebase 的意义。

了解其基本过程后，我们就可以是用 rebase 命令开始进行合并分支的操作：

1. 在项目中执行 git rebase master，如下所示。因为两次提交都存在冲突，故在 rebase 工作区中需要依次解决这些冲突。

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ea461116e8a249d59459908da733654e~tplv-k3u1fbpfcp-watermark.awebp)

在 feature 分支上执行 gitk 命令，可以在界面中看到：

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7224c03f13f340ce989942e4c33b0e16~tplv-k3u1fbpfcp-watermark.awebp)

1. feature 分支完成变基之后，切换回 master 分支执行 git merge feature，就可以完成合并操作。

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/04422f1b687d4f18a780533584df29bf~tplv-k3u1fbpfcp-watermark.awebp)

在 master 分支上执行 gitk，其分支结构如下。可以看到分支呈现一条线，看上去非常清爽。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/203b1ce49781403e938e2e515a044e7d~tplv-k3u1fbpfcp-watermark.awebp)

## git stash

有时候分支上的代码还没开发完成，需要合并分支，此时只需要：

1. 执行 git stash 将工作区内容存储起来，然后选择上述两种合并分支的方式进行分支合并。

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/100527788f1b40a1ae9c32b9b0a5311f~tplv-k3u1fbpfcp-watermark.awebp)

1. 完成分支合并后，切回开发的分支，执行 git stash pop 将工作区内容弹出就可以继续愉快的写代码了。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0017237fd1cb49cbb3f7fd36bb472d4f~tplv-k3u1fbpfcp-watermark.awebp)

## 总结

git merge 比较粗暴，也是大多数会选择的方式，这种方式可以保证每个 commit 都按照时间顺序排列，但是分支图会非常凌乱，而会引入一次没有意义的 commit。

git rebase 在历史提交记录就是一条线，非常优雅，但存在修改历史 commit 的风险，并且 git log 查看日志时 commit 时间线错乱。

个人倾向于使用 rebase 方法，毕竟 commit 的认知成本摆在那里，而且看着也舒服。不过如果开发人员很多，还是 merge 吧，毕竟一个个解决冲突会烦死个人，哈哈哈
