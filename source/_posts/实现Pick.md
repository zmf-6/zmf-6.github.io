---
title: 实现Pick
date: 2023-06-12 16:42:45
tags: ["TS"]
---

### 实现Pick(中文)

------



```tsx
type MyPick<T, K extends keyof T> = {
  [key in K]: T[key]
}
```

这里和说明一下**keyof** 及 **in** 的概念及用法，避免刚接触的小伙伴查找。

##### keyof: 取interface的键后保存为联合类型

```tsx
interface userInfo {
  name: string
  age: number
}
type keyofValue = keyof userInfo
// keyofValue = "name" | "age"
```

##### in: 取联合类型的值，主要用于数组和对象的构建

```tsx
type name = 'firstname' | 'lastname'
type TName = {
  [key in name]: string
}
// TName = { firstname: string, lastname: string }
```

切记不要用于interface, 否则会报错

##### 用于实际开发，举个例子：

```tsx
function getValue(o:object, key: string){
  return o[key]
}
const obj1 = { name: '张三', age: 18 }
const values = getValue(obj1, 'name')
```

这样写丧失了ts的优势：

1. 无法确定返回值类型
2. 无法对key进行约束

```tsx
function getValue<T extends Object,K extends keyof T>(o: T,key: K): T[K] {
  return o[key]
}
const obj1 = { name: '张三'， age: 18}
const values = getValue(obj1, 'name')
// 如果第二个参数不是obj1中的参数就会报错
```

