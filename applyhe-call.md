# apply\(\)和call\(\)

##### 作用

`call` 和 `apply` 都是为了改变某个函数运行时的 context 即上下文而存在的，换句话说，就是为了**改变函数体内部 this 的指向**。

##### 方法定义

`call` 和 `apply`二者的作用完全一样，只是接受参数的方式不太一样。

###### 方法

```js
/*apply()方法*/
function.apply(thisObj[, argArray])

/*call()方法*/
function.call(thisObj[, arg1[, arg2[, [,...argN]]]]);
```

###### 定义

**apply**：应用某一对象的一个方法，用另一个对象替换当前对象。例如：`B.apply(A, arguments);`即A对象应用B对象的方法。

**call**：调用一个对象的一个方法，以另一个对象替换当前对象。例如：`B.call(A, args1,args2);`即A对象调用B对象的方法。

> PS:A对象将代替B类里的this对象

##### 异同之处

###### 相同

都“可以用来代替另一个对象调用一个方法，将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象”。

###### 不同

**apply**：**最多只能有两个参数**——新this对象和一个数组argArray。如果给该方法传递多个参数，则把参数都写进这个数组里面，当然，即使只有一个参数，也要写进数组里。如果argArray不是一个有效的数组或arguments对象，那么将导致一个TypeError。如果没有提供argArray和thisObj任何一个参数，那么Global对象将被用作thisObj，并且无法被传递任何参数。

**call**：它**可以接受多个参数**，第一个参数与apply一样，后面则是一串参数列表。这个方法主要用在js对象各方法相互调用的时候，使当前this实例指针保持一致，或者在特殊情况下需要改变this指针。如果没有提供thisObj参数，那么 Global 对象被用作thisObj。

实际上，`apply`和`call`的功能是一样的，只是传入的参数列表形式不同。

##### 严格模式和非严格模式

###### 非严格模式

在非严格模式下当我们第一个参数传递为**null**或**undefined**时，函数体内的`this`会指向默认的宿主对象，在浏览器中则是`window`

```js
'use strict'
var test = function(){
    console.log(this===window);
}
test.apply(null);//true
test.call(undefined);//true
```

###### 严格模式

在**ECMAScript 5**的**strict**模式下，这种情况下的**this**已经被规定为不会指向全局对象，而是**undefined**

```js
'use strict'
var test = function(){
    console.log(this===window);
    console.log(this===undefined);
}
test.apply(null);
test.call(undefined);
//result:false false false true
```

##### 用法

###### 借用别人的方法

此时**foo**中的**logName**方法将被**bar**引用 ，**this**指向了**bar**

```js
'use strict'
var Animal = {
    name:"goat",
    logName:function(){
      console.log(this.name);
    }
}
var Sheep = {
    name:"sheep"
}
Animal.logName.apply(Sheep);
Animal.logName.call(Sheep);
// result:
// > sheep
// > sheep
```

###### 实现继承

> 单一继承
>
> ```js
> 'use strict'
> function Animal(name){
>     this.name = name;
>     this.logName = function(){
>       console.log(this.name);
>     }
> }
> function Sheep(name){
>     Animal.call(this,name);
>     //apply的用法
>     //Animal.apply(this,[name]);
> }
> var sheep = new Sheep("sheep");
> sheep.logName();
> ```

> 多重继承
>
> ```js
> 'use strict'
> function Cat(){
>     this.logName = function(name){
>       console.log(name);
>     }
> };
> function Dog(){
>     this.showName = function(name){
>       console.log(name);
>     }
> };
> function Animal(){
>     Cat.call(this);
>     Dog.call(this);
>     //Cat.apply(this);
>     //Dog.apply(this);
> };
> var a = new Animal();
> a.logName("Cat");
> a.showName("Dog");
> ```

##### 实际中的问题

在实际开发中，经常会遇到this指向被不经意改变的场景。  
有一个局部的`fun`方法，`fun`被作为普通函数调用时，`fun`内部的this指向了`window`，但我们往往是想让它指向该`#test`节点，见如下代码：  
~~'use strict'~~

```js
window.id="window";
document.querySelector('#test').onclick = function(){
  console.log(this.id);//test
  var fun = function(){
    console.log(this.id);
  }
  fun();//window
}
```

在严格模式下，就会出现问题。

> test  
> 15:33:34.798 index.js:7 Uncaught TypeError: Cannot read property 'id' of undefined at fun \(index.js:7\) at HTMLButtonElement.document.querySelector.onclick \(index.js:9\)

使用**call**,**apply**我们就可以轻松的解决这种问题了

```js
'use strict'
window.id="window";
document.querySelector('#test').onclick = function(){
  console.log(this.id);//test
  var fun = function(){
    console.log(this.id);
  }
  fun.call(this);//test
  fun.apply(this);//test
}
```

当然你也可以这样做，不过在**ECMAScript 5**的**strict**模式下，这种情况下的**this**已经被规定为不会指向全局对象，而是**undefined**：

```js
'use strict'
window.id="window";
document.querySelector('#test').onclick = function(){
  var that = this;
  console.log(this.id);//test
  var fun = function(){
    console.log(that.id);
  }
  fun();//test
}
```

##### 更多巧妙的用法

###### 数组类

通常把具有一下条件的对象称为数组类  
1. 具有length属性  
2. 按索引方式存储数据  
3. 不具有数组的push,pop等方法  
常见类数组有 **arguments**,**NodeList**!

```js
(function(){
    Array.prototype.push.call(arguments,4);
    console.log(arguments);//[1, 2, 3, 4]
})(1,2,3);
```

这样就往**arguments**中push一个4进去了

同样push方法没有提供push一个数组,但是它提供了`push(param1,param,…paramN)` 所以同样也可以通过**apply**来装换一下这个数组,即:

```js
var arr1=new Array("1","2","3"); 
var arr2=new Array("4","5","6"); 
Array.prototype.push.apply(arr1,arr2); 
console.log(arr1);//["1", "2", "3", "4", "5", "6"]
```

###### 求数组中的最大\(小\)值

因为`Math.max`不支持`Math.max([param1,param2])`也就是数组，但是它支持`Math.max(param1,param2...)`，所以可以根据**apply**的特点来解决 `var max=Math.max.apply(null,array)`，这样就轻易的可以得到一个数组中的最大项（apply会将一个数组转换为一个参数接一个参数的方式传递给方法）

这块在调用的时候第一个参数给了**null**，这是因为没有对象去调用这个方法，我只需要用这个方法帮我运算，得到返回的结果就行，所以直接传递了一个**null**过去。

```js
var arr = [2,3,54,32,6,99,34];
var  maxVal = Math.max.apply(null,arr);
console.log(maxVal);//99
```

###### 判断类型

```js
console.log(Object.prototype.toString.call(123)) //[object Number]
console.log(Object.prototype.toString.call('123')) //[object String]
console.log(Object.prototype.toString.call(undefined)) //[object Undefined]
console.log(Object.prototype.toString.call(true)) //[object Boolean]
console.log(Object.prototype.toString.call({})) //[object Object]
console.log(Object.prototype.toString.call([])) //[object Array]
console.log(Object.prototype.toString.call(function(){})) //[object Function]
```



