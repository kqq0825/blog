
```js
let a = Array.from({length:1});
let b = new Array(1); 
let c = Array.of(1);
console.log(a,b,c)
```
#### 输出:
> [undefined] [empty] [1] 

#### Array.from()
```js
let a = Array.from({length:1});
//以下例子获取到对应数字的索引
let aaa = Array.from({length:10});
console.log(Object.keys(aaa))
//["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]
```
1.Array.from 这个方法主要用于将对象转化为真正的数组。可转化的对象主要分为几类：
1-1 dom合集或者函数的arguments对象function foo() {
  var args = Array.from(arguments);
}
1-2 可遍历的对象，拥有Iterator 接口的数据结构Array.from(new Set([1,2,3]))
1-3 类似数组的对象，即拥有length属性的对象Array.from({length:1})
Array.from 会为数组的每个元素开辟存储空间，但是每个元素未赋值，所以对应的值为undefined。


#### new Array()

```js

let b = new Array(1) 
//以下对应的keys为空所以证明索引还未定义
console.log(Object.keys(b))//[]

```
通过调用构造函数来生成数组，当构造函数的参数数量为1个时，
这个参数代表的含义为创建一个长度为1的数组Array()构造函数会为创建的数组申请一个存储空间，
但这个空间中没有元素的存储值，元素对应的索引也未定义也就是并未给数组的每个元素开辟存存储空间所以c对应的值是一个长度为1的空数组。
上述代码`console.log(Object.keys(b))`的值是[]，也进一步说明了元素及元素的索引都未定义的情况。

```js
let d = new Array(1,2,3)
//等同于let d = [1,2,3]
```
而当构造函数的参数数量大于一个时，参数代表数组的元素。

#### Array.of()

Array.of()方法就和new Array()的使用大致相同，但是弥补了new Array()参数数量不同时产生不同结果。
所以当Array.of()的参数为1个时，也是生成一个长度为1且值为参数的数组，即[1]。
