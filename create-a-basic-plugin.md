# Create a Basic Plugin

##### jQuery 的开发方式

1. 通过`$.extend()`来扩展jQuery
2. 通过`$.fn`向jQuery添加新方法
3. 通过`$.widget()`应用jQuery UI的部件工厂方式创建

##### 写在哪里

写插件一般都是单独的一个文件出来，然后可重复的供他人调用。由于插件依赖的是jQuery，所以在写插件的时候需要避免一些不必要的冲突和一些兼容的问题，所以就有了一下的一种安全的结构。

```js
;(function($,window,document,undefined){
    //CODE HERE
})(jQuery,window,document);
```

#### $.extend\(\)

> 第一种方式很简单，仅仅是在jQuery命名空间或者理解成jQuery身上添加了一个静态方法而以。所以我们调用通过$.extend\(\)添加的函数时直接通过$符号调用（$.myfunction\(\)）而不需要选中DOM元素\($\('\#example'\).myfunction\(\)\)。

例子：

```js
$.extend({
    sayHello: function(name) {
        console.log('Hello,' + (name ? name : 'Dude') + '!');
    }
})
$.sayHello(); //调用
$.sayHello('Linfs'); //带参调用
```

运行结果：

> Hello,Dude!  
> Hello,Linfs

第一种方式很简单，但是也有很大的局限性。这种方式无法利用jQuery强大的选择器带来的便利，要处理DOM元素以及将插件更好地运用于所选择的元素身上，还是需要使用第二种开发方式

#### $.fn

##### 基本格式

```js
$.fn.pluginName = function(){
    //CODE HERE
}
```

#### 简单的例子

##### 给链接上色

```js
$.fn.greenify = function() {
    this.css( "color", "green" );
};
// 调用
$( "a" ).greenify();
```

通过以上的插件方法就可以把所有的链接变成绿色了。

插件里面的`this`主要代表的就是**所选元素的一个集合**，也就是`$("a")`，即this=$\("a"\),相当于`$("a").css( "color", "green" )`。

上面说了`this`是所选元素的一个集合，但是有时候并不需要对所有的元素进行同样的操作，所以接下来将处理集合中的每个元素。

##### each\(\)

使用jQuery中的each\(\)对集合中的元素进行操作，这时候each\(\)内部的this指带的是普通的DOM元素了，如果需要调用jQuery的方法那就需要用$来重新包装一下

```js
;(function($,window,document,undefined){
    var colorArr = ["#3793e2","#5ab55a","#cc3f65","#a526cb"];
    $.fn.changeColor = function(){
        this.each(function(){
            var i = Math.round(Math.random()*(colorArr.length-1));
            $(this).css({"color":colorArr[i]});
        });
    }
})(jQuery,window,document);

//调用
$("a").changeColor();
```

运行结果：  
![](/assets/20170914143934.png)

这样就随机的给每一条链接配上颜色，而不是同样的颜色。

##### 支持链式调用

看到上面的结果，还不是很美观，如果能去掉下划线就ok了。这时候要在原来的基础上调用其它的方法将下划线出去掉，就要用到链式调用了。如果按照刚才的写法是无法完成链式调用的，要让插件不打破这种链式调用，只需return一下即可。

```js
;(function($,window,document,undefined){
    var colorArr = ["#3793e2","#5ab55a","#cc3f65","#a526cb"];
    $.fn.changeColor = function(){
        return this.each(function(){
            var i = Math.round(Math.random()*(colorArr.length-1));
            $(this).css({"color":colorArr[i]});
        });
    }
})(jQuery,window,document);

//调用
$("a").changeColor().css("text-decoration","none");
```

运行结果：  
![](/assets/20170914144849.png)

##### 接收参数

这是后你会发现，简单的改变字体的颜色已经满足不了你的需求了，你需要改变更多的元素属性，这时候我们设置更多的属性接收不同的参数来满足需求。  
看例子：

```js
;(function($,window,document,undefined){
    $.fn.changeColor = function(options){
        var defauts = {
          "colorArr":['#3793e2','#5ab55a','#cc3f65','#a526cb'],
          "backgroundColor":"#eee",
          "fontSize":"14px"
        };
//      var settings = $.extend(defauts,options);
        var settings = $.extend({},defauts,options);
        return this.each(function(){
            var i = Math.round(Math.random()*(settings.colorArr.length-1));
            $(this).css({
                "color":settings.colorArr[i],
                "backgroundColor":settings.backgroundColor,
                "fontSize":settings.fontSize
            });
        });
    }
})(jQuery,window,document);
// 使用默认参数的调用
$("a").changeColor().css("text-decoration","none");
// 修改默认参数的调用
$("a").changeColor({
    "colorArr":['#3793e2','#5ab55a','#cc3f65','#a526cb',"#fcbe16","#0afafa"],
    "backgroundColor":"#000",
    "fontSize":"16px"
}).css("text-decoration","none");
```

| 使用默认参数的调用 | 修改默认参数的调用 |
| :--- | :--- |
| ![](/assets/20170914151500.png) |![](/assets/20170914152017.png)|

看完代码会发现有两种接收参数的方式。
1. `var settings = $.extend(defauts,options);`这种方式有个特点，就是options带进来的值会覆盖掉defaults的默认值，这样如果需要再调用默认值的话会变成传进来的值。
![](/assets/20170914153043.png)
2. `var settings = $.extend({},defauts,options);`这个多了个对象，这样所有值被合并到这个空对象上，保护了插件里面的默认值，可以保证传进来的值覆盖原来的默认值。
![](/assets/20170914154701.png) 
  
所以，一般来说都会使用第二种方式传递参数。

####面向对象插件开发

未完待续。。。
