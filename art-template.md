#art-template
######高效的javascript模版引擎

#####简介

[artTemplate](https://aui.github.io/art-template/) 是新一代 javascript 模板引擎，它采用预编译方式让性能有了质的飞跃，并且充分利用 javascript 引擎特性，使得其性能无论在前端还是后端都有极其出色的表现。在 chrome 下渲染效率测试中分别是知名引擎 Mustache 与 micro tmpl 的 25 、 32 倍。

![](/assets/2.png)
![](/assets/1.png)

#####特性

* 拥有接近 JavaScript 渲染极限的的性能
* 调试友好：语法、运行时错误日志精确到模板所在行；支持在模板文件上打断点（Webpack Loader）
* 支持压缩输出页面中的 HTML、CSS、JS 代码
* 支持 Express、Koa、Webpack
* 支持模板继承与子模板
* 兼容 EJS、Underscore、LoDash 模板语法
* 模板编译后的代码支持在严格模式下运行
* 支持 JavaScript 语句与模板语法混合书写
* 支持自定义模板的语法解析规则
* 浏览器版本仅 6KB 大小

#####IE8的兼容
```html
<script type="text/javascript" src="compatible/es5-shim.min.js"></script>
<script type="text/javascript" src="compatible/es5-sham.min.js"></script>
<script type="text/javascript" src="compatible/json3.min.js"></script>
```
文件下载：[es5-sham.min.js](https://github.com/linfushan/FILES/blob/master/arttemplate/compatible/es5-sham.min.js)、[es5-shim.min.js](https://github.com/linfushan/FILES/blob/master/arttemplate/compatible/es5-shim.min.js)、[json3.min.js](https://github.com/linfushan/FILES/blob/master/arttemplate/compatible/json3.min.js)

#####文件下载
[art-template](https://github.com/linfushan/FILES/blob/master/arttemplate/template-web.js)
#####语法支持（标准语法和原始语法）
art-template 同时支持两种模板语法。标准语法可以让模板更容易读写；原始语法具有强大的逻辑处理能力。
######标准语法
```html
{{if user}}
  <h2>{{user.name}}</h2>
{{/if}}
```
######原始语法
```html
<% if (user) { %>
  <h2><%= user.name %></h2>
<% } %>
```
######模版渲染
```js
var template = require('art-template');
var html = template(__dirname + '/tpl-user.art', {
    user: {
        name: 'linfs'
    }
});
```
#####简单的使用
```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>art-template</title>
    <!--兼容IE8-->
    <script type="text/javascript" src="compatible/es5-shim.min.js"></script>
    <script type="text/javascript" src="compatible/es5-sham.min.js"></script>
    <script type="text/javascript" src="compatible/json3.min.js"></script>
    <!--end-->
    <script type="text/javascript" src="template-web.js"></script>
</head>
<body>
    <div id="content"></div>
    <script id="test" type="text/html">
    {{if isAdmin}}
        <h1>{{title}}</h1>
        <ul>
            {{each list value i}}
                <li>索引 {{i+1}} : {{value}} </li>
            {{/each}}
        </ul>
    {{/if}}
    {{$data}}
    </script>
    <script type="text/javascript">
        var data = {
            title: '基本例子',
            isAdmin: true,
            list: ['文艺', '博客', '摄影', '电影', '民谣', '旅行', '吉他']
        };
        var html = template('test', data);
        document.getElementById('content').innerHTML = html;
    </script>
</body>
</html>
```
运行结果：
![](/assets/3.png)
#####更多内容参考
[官方文档](https://aui.github.io/art-template/docs/)