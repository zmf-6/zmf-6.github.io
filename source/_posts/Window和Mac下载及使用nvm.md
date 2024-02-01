---
title: Window和Mac下载及使用nvm
date: 2024-02-01 14:50:10
tags: ["nvm"]  
---

# Window和Mac下载及使用nvm

#### 一、NVM简介

在项目开发过程中，使用到vue框架技术，需要安装node下载项目依赖，但经常会遇到node版本不匹配而导致无法正常下载，重新安装node却又很麻烦。为解决以上问题，nvm：一款node的版本管理工具，能够管理node的安装和使用，使用简单，可下载指定node版本和切换使用不同版本，方便了node的使用。

#### 二、NVM安装（Window系统）

##### 2.1 下载

安装包下载地址：

```
https://github.com/coreybutler/nvm-windows/releases
```


windows系统下载nvm-setup.zip安装包

![image-20240201145934774](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201145934774.webp)



##### 2.2 安装

双击nvm-setup.exe开始安装（安装之前最好卸载计算机已经安装的node）

![image-20240201150109318](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150109318.webp)




选择nvm安装根路径

![image-20240201150041209](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150041209.webp)




指定nodejs的安装路径（最好提前新建nodejs文件夹，在安装时选择)

![image-20240201150136992](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150136992.webp)



##### 2.3 测试

打开命令行，输入nvm -v 可查看版本,即安装成功

![image-20240201150157756](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150157756.webp)



#### 三、NVM安装（Mac系统）

在终端执行安装命令

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

后边的这个v0.33.8是nvm的版本号

等命令跑完之后，退出终端 重新打开

成功：

然后执行nvm 看看有没有反应，如果刷刷刷出一坨代码，并且最底下提示Node [Version](https://so.csdn.net/so/search?q=Version&spm=1001.2101.3001.7020) Manager ，就说明安装成功了

##### 3-1、失败问题：在mac上“[curl](https://so.csdn.net/so/search?q=curl&spm=1001.2101.3001.7020): (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused”-安装NVM

安装失败的可能原因是没有初始化Xcode

我在网上找了很多资料https://raw.githubusercontent.com/Homebrew/install/master/install说的都是打开着个网址，我打不开
所以下面是我的解决办法:

###### 1.打开网站https://www.ipaddress.com/

###### 2.查询一下 raw.githubusercontent.com对应的IP 地址

###### 3.替换系统的host文件

![image-20240201151534025](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201151534025.webp)

###### 4 写上： 199.232.68.133 raw.githubusercontent.com

###### 5.重新执行第一章的命令，进行重新安装。



##### 3-2、失败问题二如果提示是：command not found: nvm，就是安装失败了。

失败原因很有可能是因为电脑里边缺少一个叫做 .bash_profile 的文件，这个文件是一个隐藏文件，目录在/Users/YourMacUserName/.bash_profile

如果你的电脑默认是不显示隐藏文件 可以通过快捷键 command+shift+.（这里有个点儿 .）来显示出来
如果你的电脑里没有这个文件 那就新建一个 ，如果有了，那就双击打开 ，把下边的代码复制粘贴进去，然后保存。

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" 
```

保存完了之后 回到终端，再次执行安装命令：

```
 curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

记得安装完之后退出 重新开打终端啊



#### 四、NVM使用

##### 4.1 设置

设置下载源，修改setting.txt

在安装根路径下编辑setting.txt

![image-20240201150220139](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150220139.webp)




添加以下两行镜像地址

node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/

![image-20240201150247792](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150247792.webp)

##### 4.2 使用

1.nvm list available // 显示可以安装的所有node.js的版本

![image-20240201150322791](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150322791.webp)




2.nvm install 16.13.1 // 安装node.js的命名 version是版本

3.nvm list //查看已安装的node.js

4.nvm use 16.13.1 // 切换到使用指定的nodejs版本

* 表示当前使用的node版本是16.13.1

![image-20240201150345688](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20240201150345688.webp)



#### 五、NVM常用命令

nvm off                     // 禁用node.js版本管理(不卸载任何东西)
nvm on                      // 启用node.js版本管理
nvm install <version>       // 安装node.js的命名 version是版本号 例如：nvm install 8.12.0
nvm uninstall <version>     // 卸载node.js是的命令，卸载指定版本的nodejs，当安装失败时卸载使用
nvm ls                      // 显示所有安装的node.js版本
nvm list available          // 显示可以安装的所有node.js的版本
nvm use <version>           // 切换到使用指定的nodejs版本
nvm v                       // 显示nvm版本
nvm install stable          // 安装最新稳定版

#### 六、NVM常见问题

###### 1.nvm use失效 无法使用node
原因：在安装nvm的时候修改了nodejs的安装路径，但安装包并未在指定路径新建nodejs

解决：在指定路径手动新建nodejs文件夹，重新安装并指定路径

###### 2.在mac和liunx系统里边 nvm use 切换的是当次版本 下次打开终端 还是之前的node版本
要想永久切换 使用nvm alias default （版本号）

参考链接： https://blog.csdn.net/itwangyang520/article/details/105621069
https://www.jianshu.com/p/c3c44a021d08

