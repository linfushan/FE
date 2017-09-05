# json字符串和json对象互转

###### json字符串

```js
var str = "{'name':'linfs','sex':'male'}";
```

###### json对象

```js
var obj = {'name':'linfs','sex':'male'};
```

##### json字符串转换为json对象

```js
var obj = eval('(' + str + ')');
// 注：ie8(兼容模式),ie7和ie6也可以使用eval()将字符串转为JSON对象，但不推荐这些方式，这种方式不安全eval会执行json串中的表达式。
或者
var obj = str.parseJSON(); 
或者
var obj = JSON.parse(str);
// 注：ie8(兼容模式),ie7和ie6没有JSON对象，推荐采用JSON官方的方式，引入json.js。 
```

这样就可以读取：

```js
obj.name
obj.sex
```

> 特别注意：如果obj本来就是一个JSON对象，那么使用eval（）函数转换后（哪怕是多次转换）还是JSON对象，但是使用parseJSON（）函数处理后会有问题（抛出语法异常）。

##### json对象转换为json字符串

```js
var last=obj.toJSONString(); //将JSON对象转化为JSON字符
或者
var last=JSON.stringify(obj); //将JSON对象转化为JSON字符
alert(last);
```

> **注意**：  
> 上面的几个方法中，除了eval\(\)函数是js自带的之外，其他的几个方法都来自**json.js**包。新版本的 JSON 修改了 API，将 **JSON.stringify\(\)** 和 **JSON.parse\(\)** 两个方法都注入到了 Javascript 的内建对象里面，前者变成了 **Object.toJSONString\(\)**，而后者变成了 String.parseJSON\(\)。如果提示找不到**toJSONString\(\)**和**parseJSON\(\)**方法，则说明您的json包版本太低。

> [http://www.json.org/](http://www.json.org/)提供了一个json.js,这样ie8\(兼容模式\),ie7和ie6就可以支持JSON对象以及其stringify\(\)和parse\(\)方法；
>
> 可以在[https://github.com/douglascrockford/JSON-js](https://github.com/douglascrockford/JSON-js)上获取到这个js，一般现在用json2.js。



