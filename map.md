# map\(\)

这里的`map`不是“地图”的意思，而是指“映射”。`[].map()`; 基本用法跟`forEach`方法类似：

```js
array.map(callback,[ thisObject]);
```

callback的参数也类似：

```js
[].map(function(value, index, array) {
  // ...
  // value 循环当前值
  // index 循环当前下标
  // array 数组
});
```

##### 循环

`map`方法的作用不难理解，“映射”嘛，也就是原数组被“映射”成对应新数组。下面这个例子是数值项求平方：

```js
var data=[1,3,4]

var Squares=data.map(function(val,index,arr){
  console.log(arr[index]==val);  // ==> true
  return val*val           
})
console.log(Squares);        // ==> [1, 9, 16]
```

或

```js
var data = [1,3,4]

function pow(x){
  return x*x;
}
data.map(pow);// ==> [1, 9, 16]
```

##### 类型转换

把`Array`的所有数字转为字符串：

```js
var arr = [1, 2, 3];
arr.map(String); // ['1', '2', '3']
```



