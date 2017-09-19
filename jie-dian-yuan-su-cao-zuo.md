#### 节点元素操作

#####插入
```js
$(selector).append(content)
$(content).appendTo(selector)

$(selector)prepend(content)
$(content).prependTo(selector)

$(selector)after(content)
$(content).insertAfter(selector)

$(selector)before(content)
$(content).insertBefore(selector)
```
主要区分：前一个是在被选元素中插入内容，后一个是将内容插入到备选元素。

#####删除
```js
remove()

//删除<ul>中第一个<li>
var $li = $("ul li:eq(0)").remove();
//将删除的节点添加到<ul>中去
$("ul").append($li);
//删除<ul>中<li>节点title属性值为name的元素节点
$("ul li").remove("li[title=name]");

empty()

//清空<ul>中所有的元素节点
$("ul").empty();
```
两者都可以删除元素，只是empty()是删除元素的子节点，可以用来清空某个元素的内容和判断元素的内容是否为空。

#####复制
```js
clone(includeEvents)
```
includeEvents为布尔值，规定了是否复制元素的所有处理事件
默认情况下，clone()函数生成的副本中不包含事件处理器

#####替换
```js
A.replaceWith(B) //用B替换A
A.replaceAll(B)  //用A替换B

$(selector).replaceWidth(content);
$(content).replaceAll(selector);
```
两者的作用基本相同，只是replaceAll()函数无法使用函数进行替换。

