---
title: Mysql增删改查语句+封装
date: 2021-09-24 11:13:28
tags: ["mysql"]
categories: Myspl
---

mysql 语句--- 增删改查

### 增（添加）：

```
INSERT INTO 表名 (字段,....) VALUES(字段值,....)
```

### 删（删除）：

```
DELECT FROM 表名 WHERE 条件
```

### 改（修改）:

```
UPDATA 表名 SET name="赵孟凡",age=44,sex="男",GradeId=1 WHERE 条件
```

### 查（查找）：

```
SELECT * FROM 表名 WHERE 条件
```

```
SELECT * FROM 表名
```

# 封装

### 查找数据：

function Mysql(table, where) {
console.log(where);
let sql = "";
let str = "";
for (let k2 in where) {
`    多个筛选条件使用  _WHERE+=k2+"='"+where[k2]+"' AND ";
   `
​ str += k2 + "=" + where[k2];
}
where !== undefined
​ ? (sql = "SELECT _ from " + table + " where " + str)
​ : (sql = "SELECT _ from " + table);
console.log(sql);
return new Promise((resolve, reject) => {
​ pool.query(sql, (error, results, fields) => {
​ if (error) {
​ reject(error);
​ return;
​ }
​ resolve(results);
​ });
});
}

### 添加数据：

let addSql = (table, datas) => {
let fields = "";
let values = "";
for (let k in datas) {
fields += k + ",";
values = values + "'" + datas[k] + "',";
}
console.log(fields, values);
fields = fields.slice(0, -1);
values = values.slice(0, -1);
console.log(fields, values);
let sql = "INSERT INTO " + table + "(" + fields + ") VALUES(" + values + ")";
return new Promise((resolve, reject) => {
pool.query(sql, (error, results) => {
if (error) {
reject(error);
return;
}
resolve(results);
});
});
};

### 修改数据：

let xiuSql = function (table, sets, where) {
let \_SETS = "";
let \_WHERE = "";
let keys = "";
let values = "";
for (let k in sets) {
\_SETS += k + "='" + sets[k] + "',";
}
\_SETS = \_SETS.slice(0, -1);
for (let k2 in where) {
// \_WHERE+=k2+"='"+where[k2]+"' AND ";
\_WHERE += k2 + "=" + where[k2];
}
// UPDATE user SET Password='321' WHERE UserId=12
//update table set username='admin2',age='55' where id="5";
let sql = "UPDATE " + table + " SET " + \_SETS + " WHERE " + \_WHERE;
console.log(sql);
return new Promise((resolve, reject) => {
pool.query(sql, (error, results) => {
if (error) {
reject(error);
return;
}
resolve(results);
});
});
};

### 删除数据：

let remSql = function (table, where) {
let \_WHERE = "";
for (let k2 in where) {
`    多个筛选条件使用  _WHERE+=k2+"='"+where[k2]+"' AND ";
   `
\_WHERE += k2 + "=" + where[k2];
}
// DELETE FROM user WHERE UserId=12
let sql = "DELETE FROM " + table + " WHERE " + \_WHERE;
return new Promise((resolve, reject) => {
pool.query(sql, (error, results) => {
if (error) {
reject(error);
return;
}
resolve(results);
});
});
};

### 抛出：

module.exports = { Mysql, addSql, xiuSql, remSql };

### 配合 koa-router 接口调用：

![image-20210924204839266](https://i.loli.net/2021/09/24/ZzcqMe6hlUICVX2.png)

### 数据库 数据格式：

![image-20210924204937049](mysql增删改查语句+封装.assets/image-20210924204937049.png)

### 宝子哥博客地址：

```
https://bingyu123.gitee.io/blog/java/base/base3/1/
```

```
https://bingyu123.gitee.io/blog/java/base/base3/2/
```
