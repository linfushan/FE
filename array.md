#Array

>JavaScript的`Array`可以包含任意数据类型，并通过索引来访问每个元素

#####声明一个数组
```js

var arr = [];
var arr = [1,2,3];
var arr = new Array();

```

#####给数组添加值和删除值
######push 和 pop
> push 在数组的尾端添加值，pop 删除数组末端的值

```js
var arr = [1,2,3];
arr.push(4,5);
arr
//result:[1,2,3,4,5]
arr.pop()
//result:[1,2,3,4]
arr.pop();
arr.pop();
//result:[1,2]
```
######unshift 和 shift
>unshift 在数组前面插入值，shift 删除数组前面的值

```js
var arr = [1,2,3];
arr.unshift(-1,0);
//result:[-1,0,1,2,3]
arr.shift();
//result:[0,1,2,3]
arr.shift();
arr.shift();
//result:[2,3]
```
#####数组的长度 length
```js
var arr = [1,2,3];
var len = arr.length;
//result:3
```
#####索引某个元素的位置 indexOf
```js
var arr = [1,2,3];
var indexPos = arr.indexOf(2);
//result:1
```
#####通过索引获取数组的值
```js
//一位数组
var arr1 = [1,2,3];
arr1[2];
//result:[3]
//二位数组
var arr2 = [1,2,3,[4,5,6]];
arr2[1][2];
//result:[6]
```
#####通过索引给数组赋值
>请注意，直接给`Array`的`length`赋一个新的值会导致`Array`大小的变化：

```js
var arr = [1,2,3];
arr.length = 5;
//result:[1,2,3,undefined,undefined]
arr.length = 2;
//result:[1,2]
```

>请注意，如果通过索引赋值时，索引超过了范围，同样会引起`Array`大小的变化：

```js
var arr = [1,2];
arr[1];
//result:[2]
arr[4] = 5;
//result:[1,2,undefined,undefined,5]
```

>大多数其他编程语言不允许直接改变数组的大小，越界访问索引会报错。然而，JavaScript的Array却不会有任何错误。在编写代码时，不建议直接修改Array的大小，访问索引时要确保索引不会越界。

#####索引(截取)某个位置的元素 slice splice
>`slice()`就是对应`String`的`substring()`版本，它截取`Array`的部分元素，然后返回一个新的`Array`

```js
var arr[0,1,2,3,4,5];
var sVal = arr.slice(2,3);
//result:[2]

```
> 注意到`slice()`的起止参数包括开始索引，不包括结束索引。

> 如果不给slice()传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个Array：

```js
var arr[0,1,2,3,4,5];
var sVal = arr.slice();
//result:[0,1,2,3,4,5]
```
>`splice()`方法是修改`Array`的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素：
`splice(删除起始位，删除的个数，[添加元素，添加元素，···])`

```js
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```

#####数组顺序调整 sort reverse

>`sort()`可以对当前`Array`进行排序，它会直接修改当前`Array`的元素位置，直接调用时，按照默认顺序排序：

```js
var arr = [1,2,3];
arr.sort();
arr;
//result:[3,2,1]
```

>`reverse()`把整个`Array`的元素给掉个个，也就是反转：

```js
var arr = [1,2,3,4];
arr.reverse();
arr;
//result:[4,3,2,1]
```
#####数组的链接 concat 和拼接 join

>`concat()`方法把当前的`Array`和另一个`Array`连接起来，并返回一个新的`Array`

```js
var arr = [1,2,3];
arr.concat([3,4,5]);
//result:[1,2,3,3,4,5]
```
>实际上，`concat()`方法可以接收任意个元素和`Array`，并且自动把`Array`拆开，然后全部添加到新的`Array`里：
**请注意，concat()方法并没有修改当前Array，而是返回了一个新的Array。**

```js
var arr = ['A','B','C'];
arr.concat(1,2,[3,4]);
//result:['A','B','C',1,2,3,4]
```

>`join()`方法是一个非常实用的方法，它把当前`Array`的每个元素都用指定的字符串连接起来，然后返回连接后的字符串：

```js
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); 
// result:'A-B-C-1-2-3'
```
>如果Array的元素不是字符串，将自动转换为字符串后再连接。


