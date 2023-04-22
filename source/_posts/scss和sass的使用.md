---
title: scss和sass的使用
date: 2021-09-24 19:49:53
tags: ["scss", "sass"]
---

# sass

### 一、什么是 SASS

SASS 是一种强化 CSS 的辅助工具，提供了许多便利的写法，大大节省了设计者的时间，使得 CSS 的开发，变得简单可维护。

---

### 二、安装和使用（VS Code 中）

#### 2.1.在 vscode 中使用

1. 下载扩展文件 ==Easy Sass==
2. 在用户设置中加入以下代码既可

`"easysass.targetDir": "./css"`

#### 2.2 在 react 中使用: **使用 create-react-app(新版)安装完项目之后。**

1. 执行**npm install sass-loader node-sass --save-dev**安装 sass 这两个相关的插件。

2. 写一个 scss 文件

```javascript
.userStTitle{ background: red; p{ font-size: 12px; span{ color: green; } } div{ display: flex; flex-direction: row; align-items: center; justify-content: center; }
}
```

3. 直接在组件中引入 scss 文件

```javascript
import {
  Button,
  Card,
  Icon,
  Input,
  Layout,
  List,
  Menu,
  Progress,
  Select,
  Popconfirm,
  Pagination,
} from "antd";
import echarts from "echarts";
import React, { Component } from "react";
import { connect } from "react-redux";
import { navChanged } from "../../action/actions";
import "../../asset/css/newCss/common.css";
import "../../asset/css/newCss/scss/user.scss";
import "../../asset/css/newCss/userlist.css";
import "../../asset/font/iconfont.css";
import "../../asset/css/newCss/scss/user.scss";
```

4. 将工程跑起来然后查看页面

注意：网上的一些教程都要去 node_modules 中找 react-scripe 中的文件进行配置。这边我是用的是最新的脚手架，没有做其他的配置，如果配置不成功有可能是脚手架版本的问题。

##### **create-react-app 版本低-create-react-app 脚手架 react 项目 scss 配置**

1. 安装 loader

```javascript
npm install sass-loader node-sass --save-dev
```

2. 找到 **node_modules/react-scripts/config/webpack.config.dev.js**和**webpack.config.prod.js**文件

3. 新增标记处（**webpack.config.dev.js**和**webpack.config.prod.js**配置相同）

```javascript
// "file" loader makes sure those assets get served by WebpackDevServer. // When you `import` an asset, you get its (virtual) filename. // In production, they would get copied to the `build` folder. // This loader doesn't use a "test" so it will catch all modules // that fall through the other loaders. { // Exclude `js` files to keep "css" loader working as it injects // it's runtime that would otherwise processed through "file" loader. // Also exclude `html` and `json` extensions so they get processed // by webpacks internal loaders. exclude: [/\.js$/, /\.html$/, /\.json$/,/\.scss$/], loader: require.resolve('file-loader'), options: { name: 'static/media/[name].[hash:8].[ext]', }, }, { test:/\.scss$/, loader:['style-loader','css-loader','sass-loader'], }, ],
```

4,重新 npm start 即可调用 scss 语法

![create-react-app使用sass,scss语法1](https://cdn.jsdelivr.net/gh/IceRain-mvc/cdn/img/58ec496e735e6fd5293d0b1de8c5037a1603443628847.png)

#### 2.3 解决 npm 报错：

`Module build failed: TypeError: this.getResolve is not a function`

**1、sass-loader 的版本过高导致的编译错误，当前最高版本是 8.x，需要退回到 7.3.1**

**运行：**

**npm uninstall sass-loader（卸载当前版本）**

**npm install sass-loader@7.3.1 --save-dev**

#### 2.4 使用

1. SASS 文件就是普通的文本文件，里面可以直接使用 CSS 语法。文件后缀名是.scss 或.sass,推荐使用.scss
2. 编写好的 scss 代码保存后，会自动在 CSS 文件夹生成对应的.css 文件和.min.css 文件
3. 在 html 文件中只需引入 CSS 文件夹下生成的 CSS 文件

---

### 三、基本用法

#### 1. 变量与插值语句

1. SCSS 允许使用 `$` 声明变量

```
$blue : #1875e7;　
div {
　color : $blue;
}
```

2. 如果变量需要镶嵌在字符串之中，就必须需要写在插值语句 `#{}` 之中

```
$side : left;
.rounded {
　　border-#{$side}-radius: 5px;
}
```

#### 2.计算功能

1. SCSS 允许在代码中使用算式

```
body {
　　margin: (14px/2);
　　top: 50px + 100px;
　　right: $var * 10%;
}
```

#### 3.嵌套

1. SCSS 允许选择器嵌套

```scss
div {
    h1 {
　　    color : red;
    }
}
```

2. 属性也可以嵌套

```scss
p {
  border: {
    color: red;
  }
  //注意 : 属性嵌套后面需要加上冒号。
}
```

3. 在嵌套的代码块内，可以使用 ==&== 引用父元素

```scss
a {
  &:hover {
    color: #ffb3ff;
  }
}
```

4. 优点: 嵌套功能避免了重复输入父选择器，而且令复杂的 CSS 结构更易于管理
5. 弊端：嵌套层级越深，编译出来的 css 代码的选择器层级也越深，会导致 css 样式冗余，并且难以维护

#### 4. 注释

SCSS 共有两种注释风格

1. ==/_ 多行注释 _/== ，会保留到编译后的文件。

2. ==// 单行注释== ，只保留在 SASS 源文件中，编译后被省略。

3. 在/\*后面加一个感叹号，表示这是"重要注释"。即使是压缩模式编译，也会保留这行注释，通常可以用于声明版权信息。

```scss
/*! 
　　重要注释！
*/
```

---

### 四、代码的重用

#### 1. 占位符%

1. SCSS 允许通过 ==%== 来声明一个选择器，但必须通过 ==@extend== 指令调用

```scss
%wh {
  width: 100px;
  height: 100px;
}

div {
  @extend %wh;
}
```

#### 2. 继承 @extend

1. SCSS 允许一个选择器，继承另一个选择器

```scss
.class1 {
  　　border: 1px solid #ddd;
}
```

2. class2 要继承 class1，就要使用 ==@extend== 命令

```scss
.class2 {
　　@extend .class1;
}
```

#### 3. 混合宏 @mixin

1. 使用 ==@mixin== 命令，定义一个可以重用的代码块。

```scss
@mixin left{
    float：left;
    margin-left:10px;
}
```

2. 使用 ==@include== 命令，调用这个混合宏。

```scss
div {
  @include left;
}
```

3. @mixin 的强大之处，在于可以指定参数和默认值。

```scss
@mixin common($w, $h, $bg: pink) {
  width: $w;
  height: $h;
  　　background: $bg;
}
```

4. 使用的时候，根据需要加入参数：

```scss
div {
  @include common(100px, 100px, red);
}
```

#### 4. 插入文件

==@import== 命令，用来插入外部文件。

```scss
@import "reset.scss";
```

### 五.高级用法

#### 1.循环语句

1. `@for $var from <start> through <end>` 含头含尾

```
@for $i from 1 through 10{
    .border-#{$i}{
        border:#{$i}px solid blue;
    }
}
```

2. `@for $var from <start> to <end>` 含头不含尾

```scss
@for $i from 1 to 4 {
  .list li {
    &:nth-child(#{$i}) {
      font-size: #{$i}0px;
    }
  }
}
```

#### 2. 自定义函数

1. `@function` 用于声明函数 `@return` 用于返回值
2. 先声明后使用

```scss
@function double($n) {
　　@return $n * 2;
}

#sidebar {
　　width: double(5px);
}
```

### scss 练习 1:

<img src="./1-1-SCSS.assets/image-20200304132420266.png" alt="image-20200304132420266" style="zoom:50%;" />

鼠标移上

<img src="1-1-SCSS.assets/image-20200304132441849.png" alt="image-20200304132441849" style="zoom:50%;" />

<img src="./1-1-SCSS.assets/image-20200304132518722.png" alt="image-20200304132518722" style="zoom:50%;" />

要求 1:

```css
设置一个 double函数 border: double(5px) solid #999
```
