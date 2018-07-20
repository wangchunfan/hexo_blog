---
title: JavaScript编码命名规范及格式规范
date: 2018-07-20 17:00:35
tags: "JavaScript"
categories: "JavaScript"
---

### 变量

- 局部变量命名采用首字母小写，其它单词首字母大写：
```js
//推荐
var printContent = 'hello world' 
//不推荐，变量名意义不明确
var objext = {};
//不推荐，变量名以类型最为前缀
var strName = 'Hello World'
//不推荐，变量名使用语义不明确的缩写
var newAC = functiono(){}
```

### 接口
- 公有接口：首字母大写
- 私有接口：首字母小写

```js
Reader.Content = function () {
    //私有变量
    var info, title;
    //私有方法
    var getContent = function () { };

    return {
        //公有属性
        ContentInfo: info,
        //公有方法
        SetTitle: function (contentTitle) {
            title = contentTitle;
        }
    }
}
```

### jQuery框架
- jQuery类型变量添加 `$` 最为前缀

```js
var $tocTitle = $('.reader-toc-title');
```
### 空格
- 函数参数逗号`,`后面加空格
- 函数名后面不加空格
- 参数`)`和`{`之间有空格
```
function Partition(data, length, start, end) {
}
```

- `for` 循环中的`;`后面加空格
```
for (var i = 0; i < 10; i++) 
```
- `=` `<` 等操作符前后加空格
```
while (x == y)
```
-  `for` `while` 等后面加空格

### 注释
- 单行注释 `//`，单独占一行，不要写在代码后面
- 多行注释`/* */`

```js
/* 文件头部信息注释 */
/*!
 * reader content v1.0
 *
 * Copyright 2018
*/
```
### 其它

-  字符串使用单引号，因为HTML中使用双引号

```
var content = '<sapn id="main_content"> ...';
```

- 左大括号不要另起一行，
```js
for(var i = 0; i < 10; i ++){
}
```
- 即使逻辑只有一行也要用大括号括起来
```js
if(false){
  return true;
}
```
- 语句结束时添加分号`;`
- JavaScript有自动插入分号的算法，但是有缺陷

>在没有添加分号的语句结束处自动添加分号
除非下一行以`[`、`(`、`+`、`-`、`/`开头则不添加分号

- 由于自动添加分号导致错误
```js
return 
{
  a + b
}
```
等价于
```js
return ;
{
  a + b
}
```
可以通过将`(`不另起一行解决
- 由于没有在该添加分号处添加导致错误
```js
var b = function()
var a = b
(function()
)()
```
等价于
```
var a = b(function())()
```

-----
参考：  `《Web前端开发最佳实践》`