---
title: js实现文件下载
date: 2021-08-22 20:45:12
tags: ["js文件下载"]
categories: js
---

# js 下载文件实现

## 前言

工作中遇到需要前端实现下载功能的地方，于是研究了一下，发布一个 npm 包方便下次使用

## 一个好用的前端下载插件 js-downloadfiles ，支持进度条

### js 文件下载

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d068e2526c344ec9b31e979e72a057af~tplv-k3u1fbpfcp-watermark.awebp)

### 图片下载 支持传入 id 做进度的显示

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5ced9c7940c9498182cc7118730dd022~tplv-k3u1fbpfcp-watermark.awebp)

### 支持传入多个文件放到压缩包里面下载

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fe542b4ed12642bebd969405a6d045a3~tplv-k3u1fbpfcp-watermark.awebp)

### 视频下载

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/279afa6b782b4a5d90f95e67397b0952~tplv-k3u1fbpfcp-watermark.awebp)

### 使用说明

> js 版本的文件下载, 如果出现跨域问题，请做服务器跨域设置

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9998a7a7ad464a16ac23c75b0c564969~tplv-k3u1fbpfcp-watermark.awebp)

## npm 包地址

js-downloadfiles： [www.npmjs.com/package/js-…](https://link.juejin.cn/?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fjs-downloadfiles)

1. 安装

```
npm i js-downloadfiles --save
```

1. 引入

```
import jsDownload from 'js-downloadfiles'
```

1. 使用和参数说明

如果是单文件下载

| 参数名称                                                                                                                         | 参数解释                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| id                                                                                                                               | 文件的 id，也可以是索引值做唯一身份识别，这里主要为了返回进度的时候，使用 id 对进度进行更改，以达到展示效果 |
| url                                                                                                                              | 当前文件的 url                                                                                              |
| name                                                                                                                             | 下载到本地时的名称，包括扩展名称,这里可以自己定义                                                           |
| progressFunBack                                                                                                                  | 进度的回调函数 返回一个对象 progress(进度) ,name,id                                                         |
| ![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5ced9c7940c9498182cc7118730dd022~tplv-k3u1fbpfcp-watermark.awebp) |                                                                                                             |

```
import jsDownload from 'js-downloadfiles'
window.download =  function(url){
  jsDownload.handleDownloadOne({
    id:12,
    url:url,
    name:'296d22c8cfbc8d60901b5af98ef.jpeg',
    progressFunBack :(res)=> {
      console.log(res,'图片进度')
    }
  })
  console.log(url,'url')
}
```

如果是多文件下载

| 参数名称        | 参数解释                                                                  |
| --------------- | ------------------------------------------------------------------------- |
| list            | 文件列表，数组格式，里面的每个对象参考单文件下载的 id ,url ,name 参数即可 |
| zipName         | 下载到本地时的名称，包括扩展名称,这里可以自己定义                         |
| progressFunBack | 进度的回调函数 返回一个对象 progress(进度) ,name,id。 使用 id 做区分      |

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/59b32b11e17d4006b667aaa3b21651a0~tplv-k3u1fbpfcp-watermark.awebp)

```
/**
 * @description: 批量下载文件到压缩包
 * @param {*}
 * @return {*}
 */
import jsDownload from 'js-downloadfiles'
window.downZip =  function(){
  jsDownload.downloadToZip({
    list: //下载的文件列表
    [
      {
        id:0, // id 用于表示唯一索引
        name:'123.jpeg', //文件名称（包括扩展名）
        url:'https://你的文件地址.jpeg' //文件下载地址
      },
      {
        id:1,
        name:'com.mp4',
        url:'https://你的文件地址.mp4'
      },
    ],
    zipName:'文件下载',
    progressFunBack :(res)=> {
      console.log(res,'zip文件下载进度，包含每个文件的当前下载进度')
    }
  })
}
```

---

1. 更新

```
npm update js-downloadfiles
```
