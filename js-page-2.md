### 浅拷贝：
对象只将最外层引用更改，而对象内的对象或者属性引用地址不更改。
Object.assign就可以实现一个简单的浅拷贝，只更改最外层的引用。


```js
let s ={name: {asd: '123'},age:10}
let d = Object.assign({}, s)
d.name.asd = '123456789'
d.age = 12
console.log(d, s)
//输出 {name: {…}, age: 12}name: {asd: "123456789"}age: 12__proto__: Object {name: {…}, age: 10}
```
### 深拷贝：
	
#### 方法一：序列化/反序列化——使用简单方便能满足绝大部分场景，但是对于特殊场景使用有问题。

1. 函数无法复制
2. 稀疏数组复制错误
3. 正则对象无法复制
4. 构造函数指向错误

    
从JSON的角度思考为何会出现这些错误：
JSON.stringify() : 将对象转化为字符串  JSON.parse():将字符串转化为对象。
这两个方法都是使用JSON作为数据交换格式，而JSON作为JS语法的子集，并不完全支持JS的所有类型。比如：

* NaN、Infinity、-Infinity序列化后的结果是null
```js
let a = {
    o:NaN,
    n:Infinity,
    m:-Infinity
}
console.log(JSON.stringify(a))
//输出：{"o":null,"n":null,"m":null}
```

* 日期对象序列化后的结果是ISO格式的日期字符串，JSON.parse()也无法还原。
```js
let d = new Date()
let d1 = JSON.stringify(d)
let d2 = JSON.parse(d1)
console.log(d1,d2)
//输出 "2020-03-10T14:42:48.688Z"2020-03-10T14:42:48.688Z
console.log(Object.prototype.toString.call(d))
console.log(Object.prototype.toString.call(d2))
//[object Date]
//[object String] 
```
* 正则对象无法复制

```js
let regObj = {
    o:new RegExp("a")
}
let regCopyObj = JSON.parse(JSON.stringify(regObj))
console.log(regCopyObj.o)
//输出：{}
```
* 对象方法无法复制
```js
let fnObj = {
    o:()=>{console.log("fnObj")}
}
let fnCopyObj = JSON.parse(JSON.stringify(fnObj))
console.log(fnCopyObj.o)
//输出：undefined
```
* 对于嵌套引用的对象会报错

* 抛弃对象的constructor，指向Object的构造函数
```js
class Cat {
    constructor(){
    }
}
let cat = new Cat()
let copyCat = JSON.parse(JSON.stringify(cat))
console.log(cat.constructor)
console.log(copyCat.constructor)
//输出
//class Cat {
//    constructor(){
//    }
//}
//ƒ Object() { [native code] }
```
* 稀疏数组处理错误
```js
let ary = [];
ary[3] = 1;
let copyAry = JSON.parse(JSON.stringify(ary))
console.log(ary[0])
console.log(copyAry[0])
//输出undefined null
```

所以，对于类型复杂的对象，用序列化和反序列化的方式来处理深拷贝并不安全。

方法二：对于每种类型的对象去特殊处理（普通的对象，数组，正则对象，日期Date）

定义一个超级复杂的对象
```js
let obj = {
    a:1,
    b:()=>{console.log("objFun")},
    c:{
        cReg:new RegExp("a"),
        aAry:[,,2]
    },
    d:new Date()
}
```
```js

```
