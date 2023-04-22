---
title: Hexo+GitHub搭建个人博客 && 绑定域名
date: 2020-07-18 12:12:35
tags: ["Hexo", "GitHub", "博客", "blog"]
---
> **本篇教程完整讲述了如何利用Hexo + GitHub搭建个人博客并且绑定自己的域名，成为自己的网站！**

#### 注意：

> 需要**GitHub账户**、 **Node **、**Git**、**Hexo** ，没有的下面是**安装教程** && **简单介绍**，如果都有可以**直接略过**哦。

### 安装

>#### 注册GitHub：
>
>​	**GitHub**是一个代码托管**云服务网站**，主要用于软件开发者存储和**管理**其**项目源代码**，且能够追踪、**记录**并**控制**用户对其**代码**的**修改**。
>
>GitHub官网：https://github.com/

有账号的话点击登录，没有就注册一个

![GitHub首页](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230419162751894.webp)

点击GitHub中的New repository创建新仓库，仓库名应该为：**GitHub账号名称**.[github.io](https://link.zhihu.com/?target=http://github.io) ，

![GitHub创建仓库](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420173553608.webp)

这是固定写法，比如我的仓库名为：

![image-20230420173938991](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420173938991.webp)

> #### 安装Git:
>
> Git是目前世界上最先进的分布式版本控制系统，用于敏捷高效地处理项目。网站在本地搭建好了，需要使用Git同步到GitHub上。从Git官网下载：[Git - Downloading Package](https://link.zhihu.com/?target=https://git-scm.com/download/win) 选择64位的安装包，下载后安装，(**下载红线圈中的就行**)

![Git官网首页](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230419165229283.webp)

window+r 然后输出 cmd 打开cmd

在命令行里输入**git**测试是否安装成功，若官网首页安装失败，可以**百度详细的Git安装教程**。

![cmd工具](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230419165646663.webp)

打开安装的Git文件，打开**git-bash**

![Git文件](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230419170323582.webp)

然后**分别粘贴**这两条命令 && **回车**

```
git config --global user.name "你的GitHub用户名"
git config --global user.email "注册GitHub使用的邮箱"
```

>#### 生成**ssh密钥文件**：

```
ssh-keygen -t rsa -C "注册GitHub使用的邮箱"
```

![Cmd命令行展示](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420163931003.webp)

找到密钥文件位置打开**复制密钥**(就是里边的**一堆字母**，可以用**记事本**打开)

然后去**GitHub**创建**SSH Key**。

点击**右上角头像**—>点击**Settings**—>点击左侧列表的**SSH and GPG keys**—>点击右上角**New SSH key**

**Title**:填写用途（例如：**typora**）

**key**:把刚刚复制的密钥粘贴到这里

然后点击底部按钮**Add SSH key**添加SSH key

![GitHub点击右上角头像](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230419205950331.webp)

![GitHub点击Settings](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420163809151.webp)

![GitHub点击SSH and GPG keys](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420163706395.webp)

这样连结就建好了，接下来要安装本地环境。

> #### 安装Node：
>
> Hexo基于Node.js，Node.js下载地址：[Download | Node.js](https://link.zhihu.com/?target=https://nodejs.org/en/download/) 下载安装包，注意安装Node.js会包含环境变量及npm的安装，安装后，在命令行中输入 node -v ，检测Node.js是否安装成功。

![image-20230420165028239](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420165028239.webp)

如果有**切换node版本**需要可以看 [**如何使用nvm切换node版本**](https://zhuanlan.zhihu.com/p/519270555)

到这里，安装Hexo的环境已经**全部搭建完成**

> #### 安装Hexo:
>
> **Hexo**就是我们的**个人博客网站的框架**
>
> Hexo官网：https://hexo.io/ 

 这里需要自己在电脑常里创建一个文件夹，可以命名为Blog，Hexo框架与以后你自己发布的网页都在这个文件夹中。创建好后，进入文件夹中，按住shift键，右击鼠标点击命令行“在此处打开powershell窗口”（有些版本是open command window here）。

要是没有就用**Git Bash Here**

![image-20230420170726731](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420170726731.webp)

在命令行中执行npm命令

```
npm install -g hexo-cli 
```

这个安装时间较长耐心等待，安装完成后，初始化我们的博客，在命令行输入：

```
hexo init blog
```

**注意**，这里的命令都是作用在刚刚创建的Blog文件夹中。

为了检测我们的**网站雏形**，分别**按顺序输入**以下三条命令：

```
hexo new test_my_site

hexo g

hexo s
```

这些命令在后面作介绍，完成后，打开浏览器输入地址：[**localhost:4000**](https://localhost:4000)

可以**看到**我们搭建的**博客首页**。

![博客首页](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420171501694.webp)

> ##### Hexo常用命令：（不理解的可以看上边的Hexo官网有介绍）

```
npm install hexo -g #安装Hexo
npm update hexo -g #升级Hexo版本
hexo init #初始化博客

hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo g == hexo generate #生成静态文件
hexo s == hexo server #启动本地服务预览
hexo d == hexo deploy #部署博客到GitHub（部署完就可以直接用线上地址查看我们的博客了，部署前必须先生成最新静态文件）

hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #删除静态文件（public文件夹就是静态文件），若是网页正常情况下可以忽略这条命令
```

> #### 推送到网站
>
> 上面只是在本地预览，接下来要做的就是就是推送网站，也就是发布网站，让我们的网站可以被更多的人访问。

在设置之前，需要解释一个概念，在blog根目录里的_config.yml文件称为**站点配置文件**，如下图:

![image-20230420172413494](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420172413494.webp)

如果**有VsCode**的可以用**VsCode**打开我们的blog文件。（没有就用记事本打开）

打开**_config.yml**滑到最底部，**找到这段代码**如下：

![image-20230420173052999](https://cdn.jsdelivr.net/gh\zmf-6\cdn@master\img\image-20230420173052999.webp)

修改：

```
deploy:
type: git
repo: 这里填入你之前在GitHub上创建仓库的完整路径，记得加上 .git
branch: main（以前是master）
```

保存站点配置文件。

> 其实就是给hexo d 这个命令做相应的配置，让hexo知道你要把blog部署在哪个位置，很显然，我们部署在我们GitHub的仓库里。

最后安装Git部署插件，输入命令：

```
npm install hexo-deployer-git --save
```

然后现在就可以**部署**我们的**博客到GitHub**了，**分别执行**这三条命令：

```
hexo clean 
hexo g 
hexo d
```

完成后，打开浏览器，在地址栏输入你的放置个人网站的仓库路径，即: **GitHub用户名.github.io**，就能在线上看到我们的博客啦。



> ### 绑定域名
>
> 虽然在Internet上可以访问我们的网站，但是网址是GitHub提供的[xxxx.github.io](https://link.zhihu.com/?target=http://xxxx.github.io) 而我们想使用我们自己的个性化域名，这就需要绑定我们自己的域名。在国内主流的域名代理厂商也就阿里云和腾讯云。

登录到阿里云，进入管理控制台的域名列表，找到你的个性化域名，进入解析，然后添加解析，包括添加三条解析记录，192.30.252.153是GitHub的地址，你也可以ping你的[github.io](https://link.zhihu.com/?target=http://xxxx.github.io) 的ip地址，填入进去。第三个记录类型是CNAME，CNAME的记录值是：**你的GitHub用户名.github.io** 这里千万别弄错了。

第二步，登录GitHub，进入之前创建的仓库，点击settings，设置Custom domain，输入你的域名，点击save保存。

第三步，进入本地博客文件夹 ，进入blog/source目录下，创建一个记事本文件，输入你的域名，对，只要写进你自己的域名即可。如果带有www，那么以后访问的时候必须带有www完整的域名才可以访问，但如果不带有www，以后访问的时候带不带www都可以访问。所以建议，不要带有www。

保存，命名为CNAME ，注意保存成**所有文件**而不是**txt文件**。

完成这三步，进入blog目录中，按住shift键右击打开命令行工具，依次输入

```
hexo clean
hexo g
hexo d
```

这时候打开浏览器在地址栏输入**你的个性化域名**将会直接进入你自己搭建的网站。

> ### 更换主题
>
> 

> #### 初识MarkDown语法
>
> Markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。Markdown语法简洁明了、容易掌握，而且功能比纯文本更强，因此写博客使用它，可以让用户更加专注的写文章，而不需要费尽心力的考虑样式，相对于html已经算是轻量级语言，像有道云笔记也支持Markdown写作。并且Markdown完全兼容html，也就是可以在文章里直接插入html代码。比如给博文添加音乐，就可以直接把音乐的外链html代码插入文章中。具体语法参看：[Markdown 语法说明]可以说十分钟就可以入门。当然，工欲善其事必先利其器，选择一个好的Markdown编辑器也是非常重要的，这里推荐Typora ，也可以使用本地的文本编辑器，更多的Markdown的语法与编辑器自己可以搜索了解。

MarkDown官网：https://markdown.com.cn/basic-syntax/

MarkDown使用参考：https://markdown.com.cn/editor/#jump_8

> ### 错误参考：

#### 一、执行hexo d的时候报如下错误

![image-20230420175709451](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20230420175709451.png)

不要慌,这个是因为**网络较慢**，多试几次或者**切换网络**就可以了

