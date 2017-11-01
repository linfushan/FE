#### IE条件注释

> IE条件注释仅对IE浏览器有用，其余的浏览器没用

| 操作符 | 含义 |
| :--- | :--- |
| lt | 小于 |
| gt | 大于 |
| lte | 小于等于 |
| gte | 大于等于 |
| ! | 不等于 |

例子：

```html
<!--[if lt IE 9]>
    // CODE HERE
<![endif]-->
```

#### 较为常用的Hack处理

| 字符 | 例子 | 说明 |
| :--- | :--- | :--- |
| \_ | \_color:red; | 只有IE6可以识别 |
| \* | \*color:red; | IE6/7可以识别 |
| \9 | color:red\9; | IE8及以下浏览器可以识别 |

#### CSS兼容前缀

```css
-o-transform:rotate(7deg);      // Opera 
-ms-transform:rotate(7deg);     // IE
-moz-transform:rotate(7deg);    // Firefox
-webkit-transform:rotate(7deg); // Chrome
transform:rotate(7deg);         // 统一标识语句
```

#### &lt; a &gt; 标签的几种状态顺序

> 很多新人在写 a 标签的样式，会疑惑为什么写的样式没有效果，或者点击超链接后，hover、active 样式没有效果，其实只是写的样式被覆盖了。

正确的a标签顺序应该是：

`link`:平常的状态

`visited`:被访问过之后

`hover`:鼠标放到链接上的时候

`active`:链接被按下的时候

#### placeholder 不兼容解决方案

```js
<input type="text" 
       value="placeholder content" 
       onfocus="this.value = '';" 
       onblur="if (this.value == '') {this.value = 'placeholder content';}">
```

#### 清除浮动最佳实践 clearfix

```css
.clearfix:after { display: block; clear: both; content: ""; visibility: hidden; height: 0; }
.clearfix { zoom: 1; }
```

#### BFC 解决边距重叠问题

当相邻元素都设置了 margin 边距时，margin 将取最大值，舍弃小值。为了不让边距重叠，可以给子元素加一个父元素，并设置该父元素为 BFC：overflow: hidden;

```html
<div class="box" id="box">
  <p>Lorem ipsum dolor sit.</p>

  <div style="overflow: hidden;">
    <p>Lorem ipsum dolor sit.</p>
  </div>

  <p>Lorem ipsum dolor sit.</p>
</div>
```

> **BFC\(Block formatting context\)**直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

#### IE双倍边距的问题

> 设置 ie6 中设置浮动，同时又设置 margin，会出现双倍边距的问题

```css
display: inline;
```

#### 解决 IE9 以下浏览器不能使用 opacity

```css
opacity: 0.5;
filter: alpha(opacity = 50);
filter: progid:DXImageTransform.Microsoft.Alpha(style = 0, opacity = 50);// 此步很少用到
```

#### 解决 IE6 不支持 fixed 绝对定位以及IE6下被绝对定位的元素在滚动的时候会闪动的问题

```css
/* IE6 hack */
*html, *html body {
  background-image: url(about:blank);
  background-attachment: fixed;
}
*html #menu {
  position: absolute;
  top: expression(((e=document.documentElement.scrollTop) ? e : document.body.scrollTop) + 100 + 'px');
}
```

#### IE6 背景闪烁的问题

问题：链接、按钮用 CSSsprites 作为背景，在 ie6 下会有背景图闪烁的现象。原因是 IE6 没有将背景图缓存，每次触发 hover 的时候都会重新加载

解决：可以用 JavaScript 设置 ie6 缓存这些图片：

```js
document.execCommand("BackgroundImageCache", false, true);
```

#### 解决 IE6 不支持 min-height 属性的问题

```css
min-height: 350px;
_height: 350px;
```

#### 让 IE7 IE8 支持 CSS3 background-size属性

> 由于 background-size 是 CSS3 新增的属性，所以 IE 低版本自然就不支持了，但是老外写了一个 htc 文件，名叫 background-size polyfill，使用该文件能够让 IE7、IE8 支持 background-size 属性。其原理是创建一个 img 元素插入到容器中，并重新计算宽度、高度、left、top 等值，模拟 background-size 的效果。

```css
html {
  height: 100%;
}
body {
  height: 100%;
  margin: 0;
  padding: 0;
  background-image: url('img/37.png');
  background-repeat: no-repeat;
  background-size: cover;
  -ms-behavior: url('css/backgroundsize.min.htc');
  behavior: url('css/backgroundsize.min.htc');
}
```

#### td 自动换行的问题

问题：`table`宽度固定，`td` 自动换行

解决：设置 Table 为 `table-layout: fixed`，td 为 `word-wrap: break-word`

#### 键盘事件 keyCode 兼容性写法

```js
function getKeyCode(e) {
  e = e ? e : (window.event ? window.event : "")
  return e.keyCode ? e.keyCode : e.which
}
```

#### 窗口大小的兼容写法

```js
// 浏览器窗口可视区域大小（不包括工具栏和滚动条等边线）
var client_w = document.documentElement.clientWidth || document.body.clientWidth;
var client_h = document.documentElement.clientHeight || document.body.clientHeight;

// 网页内容实际宽高（包括工具栏和滚动条等边线）
var scroll_w = document.documentElement.scrollWidth || document.body.scrollWidth;
var scroll_h = document.documentElement.scrollHeight || document.body.scrollHeight;

// 网页内容实际宽高 (不包括工具栏和滚动条等边线）
var offset_w = document.documentElement.offsetWidth || document.body.offsetWidth;
var offset_h = document.documentElement.offsetHeight || document.body.offsetHeight;

// 滚动的高度
var scroll_Top = document.documentElement.scrollTop||document.body.scrollTop;
```

#### DOM 事件处理程序的兼容写法（能力检测）

```js
var eventshiv = {
    // event兼容
    getEvent: function(event) {
        return event ? event : window.event;
    },

    // type兼容
    getType: function(event) {
        return event.type;
    },

    // target兼容
    getTarget: function(event) {
        return event.target ? event.target : event.srcelem;
    },

    // 添加事件句柄
    addHandler: function(elem, type, listener) {
        if (elem.addEventListener) {
            elem.addEventListener(type, listener, false);
        } else if (elem.attachEvent) {
            elem.attachEvent('on' + type, listener);
        } else {
            // 在这里由于.与'on'字符串不能链接，只能用 []
            elem['on' + type] = listener;
        }
    },

    // 移除事件句柄
    removeHandler: function(elem, type, listener) {
        if (elem.removeEventListener) {
            elem.removeEventListener(type, listener, false);
        } else if (elem.detachEvent) {
            elem.detachEvent('on' + type, listener);
        } else {
            elem['on' + type] = null;
        }
    },

    // 添加事件代理
    addAgent: function (elem, type, agent, listener) {
        elem.addEventListener(type, function (e) {
            if (e.target.matches(agent)) {
                listener.call(e.target, e); // this 指向 e.target
            }
        });
    },

    // 取消默认行为
    preventDefault: function(event) {
        if (event.preventDefault) {
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    },

    // 阻止事件冒泡
    stopPropagation: function(event) {
        if (event.stopPropagation) {
            event.stopPropagation();
        } else {
            event.cancelBubble = true;
        }
    }
};
```

#### 垂直居中

```html
/*
  此方法兼容所有的浏览器
*/

<style media="screen">
  *{margin: 0;padding: 0;}
  .parent{
    width: 200px;
    height: 200px;
    border: 1px solid #eee;

    *font-size:175.44px;/*在IE6/7中使用 200/1.14=175.44*/
    /*IE8及以上和其它浏览器使用此方法*/
    display: table-cell;
    vertical-align: middle;
    /*---------------------------*/
    text-align: center;
  }
  .child{
    height: 50px;
    width: 50px;
    border: 1px solid #f60;

    display: inline-block;/*text-align:center对块元素无用*/
    /*在IE6/7中实现inline-block*/
    *vertical-align: middle;
    *zoom:1;
    /*------------------------*/
    *display: inline;/*此句结合font-size使用*/
  }
</style>
<body>
  <div class="parent">
    <div class="child"></div>
  </div>
</body>
</html>
```



