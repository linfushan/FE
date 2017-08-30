# requirejs的简单使用

##### 对浏览器的支持

IE 6+ .......... compatible ✔  
Firefox 2+ ..... compatible ✔  
Safari 3.2+ .... compatible ✔  
Chrome 3+ ...... compatible ✔  
Opera 10+ ...... compatible ✔

##### 下载文件

下载地址：[GitHub-requirejs](https://github.com/linfushan/FILES/blob/master/require.js)

##### 项目目录
>requirejs
>--/js
>------/main.js
>--/scripts
>------/require.js
>------/jquery-3.2.1.min
>--/index.html

##### 导入文件

```html
<script src="scripts/require.js" data-main="js/main"></script>
```
##### main.js配置
```js
requirejs.config({
	baseUrl:'scripts/',//基础路径
	paths:{
		jquery:"jquery-3.2.1.min"//路径下的文件名不需要加后缀
	},
	shim:{//依赖模块
		//'文件名':['被依赖文件']
	}
});
define(["jquery"],function($){
	$("button").click(function(){
		alert("success");
	});
});
```



