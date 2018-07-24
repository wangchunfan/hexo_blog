---
title: ES6实用新特性
date: 2018-07-22 23:17:45
tags: "JavaScript"
categories: "JavaScript"
---

最实用的ES6新特性

## 兼容性

http://kangax.github.io/compat-table/es5/
http://kangax.github.io/compat-table/es6/

- ES6(ES2015)兼容环境: 
`IE10以上，Chrome、FireFox、移动端、NodeJS`
- 在低版本环境中使用的解决方案：
  1 在线转换 `brower.js`
  2 提前编译

## ES6新特性
1. 变量
2. 函数
3. 数组
4. 字符串
5. 面向对象
6. Promise
7. generator/yield(对Promise的封装)
8. 模块化

## 一、变量
`var` 的缺陷：

1.可以重复声明
```js
var a = 1;
var a = 2; 
```
2.无法限制修改
常量：`PI`
3.没有块级作用域

`let、const`的特性
1. 不能重复声明
2. 声明可以修改的变量/不可修改的常量
3. 拥有块级作用域`{}`

## 二、箭头函数
对函数的简写
```
() => {

}
```
**特点：**
1. 如果只有一个`参数`， `()` 可以省略
2. 如果函数块中只有一个 `return`这一行代码， `{}` 可以省略
```js
let show = a => a * 2;
alert(show(1));
```

## 三、函数参数
**三个点 `...`**
`... + 数组名 = 数组名[0] ,数组名[1] ,数组名[2], ..,数组名[length-1] }`，作为参数时互相转换 
1. 扩展形数，接收剩余参数，`...args`必须是最后一个参数
```js
function show(a, b, ...args) {
    alert(a);
    alert(b);
    alert(args);  //3,4,5   args是一个数组
}

show(1, 2, 3, 4, 5)  
```
**展开实参**
```js
function show(a, b, c) {
    alert(a);
    alert(b);
    alert(c);
}
let arr = [1, 2, 3]
//show(1, 2, 3)
show(...arr)
```
**默认参数**
```js
function show(a, b = 2, c = 3) {
    alert(a)
    alert(b)
    alert(c)
}
show(1,5)
```
## 四、解构赋值

1. 必须是声明且赋值语句
2. 等号左右两边结构必须相同
3. 右边必须是值
4. 写法形式数组`[]`和JSON字符串`{}`
5. 解构`赋值`，`赋值`也很关键

**数组形式**
```js
let [a, b] = [1, [2]];  //同时声明数组a、b并且赋值
console.log(a, b);  //  1, [2]
```

- 右边是JSON字符串形式

相比数组写法，左边是`a、b`右边也必须是 `a 和 b`，写法：`a: + 值` 和 `b: + 值` 。如果是 `c: + 值` 和 `d: + 值`，那么 `a`、`b` 的值为
 `undefind`，相当于只是声明了`a和b`
```
let {a, b, c} = {a: 1, b: [2],c: {c: 3}};
console.log(a, b, c);  //  1, [2], {c: 3}
```
- 两者结合
```js
let [{a, b} ,[c, d], e] = [{a: 1,b: 2}, ['3', ['d']],'e'] 
console.log(a, b, c, d, e);  //  1 2 "3" ["d"] "e"
```
- 注意点

**错误1：**只能是`[]``中包含`{}`，不然没法写，会报错，因为最外层就决定了最大的基调是`变量 : 值`的形式，`[b]`的变量不知道是什么
```js
let {a,[b]} = {a: 1, :[2]]};  //报错
console.log(a, b);
```
总结：左边声明多个变量，右边用不同写法为变量赋值，可以赋值任意类型
**错误2：** 
```
let [a, b] = {a: 1 ,b: 2}  //  结构不同 报错 Uncaught TypeError: {(intermediate value)(intermediate value)} is not iterable
let [a, b] = [a: 1 ,b: 2]  //  写法错误 报错 Uncaught SyntaxError: Unexpected token :
let {a, b} = {1 , 2}  //  写法错误 Uncaught SyntaxError: Unexpected token ,
```
**错误3：**声明和赋值不在一起
```js
let [a, b];  //  没有这样的声明变量方式
[a, b] = {a: 1 ,b: 2}    // Uncaught SyntaxError: Missing initializer in destructuring declaration
```
## 五、数组
- map，返回新数组，function依次操作数组元素，返回新数组元素
`arr` 调用map函数的数组
`thisValue` 在函数体中的this
```
var array = [1, 2, 3];
var thisValue = '4';
var newArray = array.map(function(value, index, arr){
    return (value + '-' + index + '-' + this + '-' + arr)
},thisValue)
console.log(newArray);  //  ["1-0-4-1,2,3", "2-1-4-1,2,3", "3-2-4-1,2,3"]
```
- reduce，汇总，从左向右每次取一个数组元素
`result` 作为每次的返回值
`thisValue` 初始值，作为循环`value`的值
```
//求和
var array = [1, 2, 3];
var thisValue = 4;
var newArray = array.reduce(function(result, value, index, arr){
    return result + value;  //下一次执行函数时，`result`参数的值

},thisValue)  //thisValue //第一次执行函数，`result`参数的值
console.log(newArray);  //  10
```
- filter过滤器
对数组array中的元素依次按条件过滤，返回新数组，true留下，false丢弃
`thisValue`,函数中this指代
```
var array = [1, 2, 3];
var thisValue = 4;
var newArray = array.filter(function(value, index, arr) {
    return value > 1 ? true : false;

}, thisValue)
console.log(newArray);  //  [2, 3]
```
- forEach迭代
```
var array = [1, 2, 3];
var thisValue = 4;
array.forEach(function(value, index, arr) {
    console.log(value + '-' + this + '-' + arr);
    //  1-4-1,2,3
    //  2-4-1,2,3
    //  3-4-1,2,3
}, thisValue)
```

## 六、字符串
- 新增方法：`startsWith(str[, position])` 
第一个参数用来比较，
第二个参数(可省略)时原字符串开始的位置,默认0。从`包含`开始位置的地方开始比较
```
var str = 'abcd';
console.log(str.startsWith('a', 0));    //true
console.log(str.startsWith('a', 1));    //false
```
- 新增方法 `endsWith(str[, position])`
从`不包含`末尾位置的地方开始
```
var str = 'abcd';
console.log(str.endsWith('d', 0));    //true
console.log(str.endsWith('d', 4));    //false 默认str.length
```
- 字符串模板
可以换行
返单引号+`${}`
```
let str = 'abcd'
let str1 = `${str}ef
g
 h` 
console.log(str1); 
//abcdef
//g
// h  输出也有一个空格

```
## 七、面向对象

### 1. 新增关键字`class`
- 旧写法
构造函数设置实例的属性
原型设置实例的方法
```
function Book(title) {
    this.title = title;
}

Book.prototype = {
    constructor: Book,
    showTitle: function() {
        console.log(this.title)
    }
}
var book = new Book('ES6');
book.showTitle(); //ES6
```
- 新写法
构造器`constructor`初始化属性
直接在类中添加方法，方法没有使用`function`关键字
```
class Book{
    constructor(title){
        this.title = title;
    }

    showTitle(){
        console.log(this.title)
    }
}

let book = new Book('ES2015')
book.showTitle();   //ES2015
```
### 2. 继承
执行父类的构造函数，使子类继承父类的属性和方法
- 旧写法
```
function MyBook(title, name) {
    Book.call(this, title);  
    this.name = name;
}
MyBook.prototype = new Book();
MyBook.prototype.constructor = MyBook;
MyBook.prototype.showName = function() {
    console.log(this.name);
}

var myBook = new MyBook('ES6', 'wangcf');
myBook.showTitle(); //ES6
myBook.showName(); //wangc
```

- 新写法

```
class Book {
    constructor(title) {
        this.title = title;
    }

    showTitle() {
        console.log(this.title)
    }
}

class MyBook extends Book {
    constructor(title, name) {
        super(title); //执行父类的构造函数
        this.name = name;
    }

    showName() {
        console.log(this.name)
    }
}

let myBook = new MyBook('ES2015', '张三')
myBook.showTitle(); //ES2015
myBook.showName(); //张三
```

## 八、JSON和对象

- 注意：JSON字符串中只能使用双引号
JSON字符串中的key必须用引号括起来
```
let obj = {
    a: 1,
    b: '2'
}
let json = JSON.stringify(obj)
console.log(json);  // {"a":1,"b":"2"}
```
- key和value变量的名字形同可以简写
```
let a = 1;
let b = 2;
let json = { a: a, b: b };
let json1 = { a, b };
console.log(json); //{a: 1, b: 2}
console.log(json1); //{a: 1, b: 2}
```
- function可以简写，省略`:function`

**旧写法**
```
let obj = {
    a: 1,
    show: function(){
        console.log(this.a);
    }
}
obj.show();  // 1
```
**新写法**
```
let obj = {
    a: 1,
    show(){
        console.log(this.a);
    }
}
obj.show();  // 1
```

## 九、Promise异步

不适用于解决下一个回调依赖上一次结果的情况
适用一次性执行多个请求，各请求之间无关
用同步的方式书写异步代码
- Promise.all 全部成功执行resolve
- Promise.race 哪个快就执行resolve

### 创建一个单一的Promise

```
let p = new Promise(function(resolve, reject){
    //异步代码
    //成功：resolve
    //失败：reject
    if(true){
        resolve('成功');
    }else{
        reject('失败')
    }
})

p.then(function(data){
    console.log(data);
},function(data){
    console.log(data);
})
// 成功
```
### 创建多个Promise
```
let p1 = new Promise(function(resolve, reject) {
    if (true) {
        resolve('成功1');
    } else {
        reject('失败1')
    }
})

let p2 = new Promise(function(resolve, reject) {
    if (true) {
        resolve('成功2')
    } else {
        reject('失败2')
    }
})

Promise.all([p1, p2]).then(function(arr) {
    //返回值是一个数组，顺序保存多个Promise返回值
    console.log('p1和p2全部resolve');
    let [data1, data2] = [arr[0], arr[1]];
    console.log(data1 + data2);
}, function(data) {
    //有一个失败就立即进入，不会继续执行其他Promise
    console.log('p1和p2其中有一个reject');
    console.log(data);
})
```
### 封装Promise
```
function createPromise(num) {
    return new Promise(function(resolve, reject) {
        if (true) {
            resolve('成功' + num);
        } else {
            reject('失败1' + num);
        }
    })
}

Promise.all([
    createPromise(1),
    createPromise(2)
]).then(function(arr) {
    //返回值是一个数组，顺序保存多个Promise返回值
    console.log('p1和p2全部resolve');
    let [data1, data2] = [arr[0], arr[1]];
    console.log(data1 + data2);
}, function(data) {
    //有一个失败就立即进入，不会继续执行其他Promise
    console.log('p1和p2其中有一个reject');
    console.log(data);
})
```

## 十、generator/yield

完美解决下一个回调依赖上一次执行结果的情况
函数组成部分：`*`和`yield`，创建`generator`对象
一般函数：一直执行到完
generator函数：可以在中间暂停,执行使用`generatro.next`
### 1.generator
```
function *show(){
    console.log(1)  //1

    yield;  // 暂停

    console.log(2)  //没有next则不执行这段子函数
}

let gen = show();
//gen.next();
gen.next();  //执行到yield暂停
```
### 2.yield
将函数分割成多个子函数
- 可以传参
- 可以有返回值，返回中间结果
```
function* show(num) {
    console.log(num); //5
    console.log(1); //1  
    let y = yield 7;    //y获取第一个子函数的结果，第一个子函数的返回值
    console.log(2); //2
    console.log(y) //4
    console.log(num) //5
    return 6;   //最后一个子函数依赖return返回
}

let gen = show(5); //第一个子函数的参数在这里传递
let res1 = gen.next(3);
let res2 = gen.next(4); //第二个next传参才可以接收
console.log(res1)   //{value: 7, done: false}
console.log(res2)   //{value: 6, done: true}
```
### 3.generator解决异步
引用runner和jQuery文件
```
runner(function *(){
    let data1 = yield $.ajax(url: xxx, dataType: 'json');
    let data2 = yield $.ajax(url: xxx, dataType: 'json');
    let data3 = yield $.ajax(url: xxx, dataType: 'json');
})
```



