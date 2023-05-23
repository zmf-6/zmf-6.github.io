---
title: promise中的异常捕获_全局
date: 2022-09-03 21:13:36
tags: ["promise"]
categories: promise
---

### 《深入理解 ES6》

###### 在 ES6 的 Promise 中，对于直接 reject 的异常未处理任务，不会进行错误提示：

```
const rejected = Promise.reject('err') // 直接报异常
```

###### 除非手动去处理一下：

```
const rejected = Promise.reject('err')

rejected.catch(function (err) {

console.log('catch', err)

})
```

###### ES6 中本身是没有提供解决方案的，但是在 Node.js 和浏览器环境中，分别提供了解决机制。

##### Node.js 端实现

> 在 node.js 端可以利用原生的 process 去监听两个事件：unhandledRejection 和 rejectionHandled；

unhandledRejection：在一轮事件循环中，当 promise 被拒绝时，会触发该事件；当 unhandledRejection 触发时，在回调函数中会创建两个参数，第一个是错误原因 (reason)，第二个是错误对象(promise)；

```

const rejected = Promise.reject('err')

process.on('unhandledRejection', function (reason, promise) {

console.log('unhandledRejection reason', reason)

console.log('unhandledRejection promise', promise)

})
```

> rejectionHandled：在一轮事件循环中，当 promise 拒绝处理后，会触发该事件；当 rejectionHandled 触发时，在回调函数中会创建一个参数，就是错误对象(promise)；

```

const rejected = Promise.reject('err')

process.on('rejectionHandled', function (promise) {

console.log('rejectionHandled promise', promise)

})
```

> 由于捕捉 rejectionHandled 与 promise.catch 不在一轮事件循环中，因此需要加个延迟处理
```

setTimeout(function () {

rejected.catch(function (err) {

console.log('catch', err)

})

}, 100)
```

> 异常追踪器思路：可以定义一个全局的定时器，然后定时扫描监听未处理 promise ，如果发现就实时处理掉。

##### 浏览器端实现

> 在浏览器端的实现，跟 node.js 端很相似，只不过是通过 window 对象来监听异常，监听方式是：onunhandledrejection 和 onrejectionhandled，与 node.js 中的 unhandledRejection 和 rejectionHandled 相对应，然后在回调函数中都只会创建一个参数，该参数是个对象类型，包含以下信息：

type：unhandledRejection 或者 rejectionHandled；

reason：错误原因；

promise：promise 对象；

同时在浏览器端也可以实现类似“异常追踪器”的功能，此处不再赘述。
