####获取类
```js
/*
* getByClass(父元素，要获取的类)
*
*/
function getByClass(oParent, sClass)
{
	var aEle=oParent.getElementsByTagName('*');
	var aTmp=[];
	var i=0;
	
	for(i=0;i<aEle.length;i++)
	{
		if(aEle[i].className==sClass)
		{
			aTmp.push(aEle[i]);
		}
	}
	
	return aTmp;
}
```

####获取样式
```js
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<script type="text/javascript">
function getStyle(obj, attr) {
	if (obj.currentStyle) {
		return obj.currentStyle[attr];
	} else {
		return getComputedStyle(obj, false)[attr];
	}
}
window.onload = function() {
	alert(getStyle(document.getElementById("div1"), 'fontSize'));
}
</script>
<body>
	<div id="div1">getStyle</div>
</body>
</html>
```

#### 浏览器默认图标favicon
```html
<link rel="Bookmark" href="favicon.ico">
<link rel="Shortcut Icon" href="favicon.ico">
```

#### js中class多种函数的封装方法

```js
<!DOCTYPE html>  
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<title>关于class的多种函数封装</title>  
<style>  
body{  
  margin: 0;  
}  
li{  
  height: 20px;  
}  
</style>  
</head>  
<body>  
<div class="box" id="box">  
  <ul class="list">  
    <li class="in abc ab "></li>  
    <li class="in ac b "></li>  
    <li class="in a "></li>  
    <li class="in acb "></li>  
    <li class="in ba "></li>  
    <li class="abc"></li>  
  </ul>  
</div>  
<script type="text/javascript">  
//数组的indexOf方法封装  
function indexOf(arr,value,start){  
  //如果不设置start,则默认start为0  
  if(arguments.length == 2){  
    start = 0;  
  }  
  //如果数组中存在indexOf方法，则用原生的indexOf方法  
  if(arr.indexOf){  
    return arr.indexOf(value,start);  
  }  
  for( var i = 0; i < arr.length; i++){  
    if(arr[i] === value){  
      return i;  
    }  
  }  
  return -1;  
}  
//数组去重方法封装  
function noRepeat(arr){  
  var result = [];  
  for( var i = 0; i < arr.length; i++){  
    if(indexOf(result,arr[i]) == -1){  
      result.push(arr[i]);  
    }  
  }  
  return result;  
}  
//inArray方法封装  
function inArray(arr,value){  
  for(var i = 0; i < arr.length; i++){  
    if(arr[i] === value){  
      return true;  
    }  
  }  
  return false;  
}  
//去除首尾空格函数封装  
function trim(arr){  
  var result = arr.replace(/^\s+|\s+$/g,'');  
  return result;  
}  
//getElementsByClassName函数封装  
function getElementsByClassName(parentObj,classStr){  
  var result = [];  
  var objs = parentObj.getElementsByTagName('*');  
    
  //如果classStr用空格分隔，则表示class必须同时满足才有效  
  var targetArr1 = noRepeat(trim(classStr).split(/\s+/));  
  //如果classStr用逗号分隔，则表示class只要有一个满足就有效  
  var targetArr2 = noRepeat(trim(classStr).split(/\s*,\s*/));  
      
  if(classStr.indexOf(',') == -1 ){  
    //用空格分隔或者只有一个class  
    label: for(var i = 0; i < objs.length; i++){  
      var arr = noRepeat(trim(objs[i].className).split(/\s+/));  
      for( var j = 0; j < targetArr1.length; j++){  
        if(!inArray(arr,targetArr1[j])){  
          continue label;  
        }  
      }  
      result.push(objs[i]);  
    }  
    return result;  
  }else{  
    //用逗号分隔  
    label: for(var i = 0; i < objs.length; i++){  
        var arr = noRepeat(trim(objs[i].className).split(/\s+/));  
        for( var j = 0; j < targetArr2.length; j++){  
          if(inArray(arr,targetArr2[j])){  
            result.push(objs[i]);  
            continue label;  
          }  
        }  
            
      }  
      return result;     
    }  
}  
    
//addclass函数封装  
function addClass(obj,classStr){  
  var array = noRepeat(trim(obj.className).split('\s+'));  
  if(!inArray(array,classStr)){  
    array.push(classStr);  
  }  
  obj.className = array.join(' ');  
  return obj;  
}  
//removeclass函数封装  
function removeClass(obj,classStr){  
  var array = noRepeat(trim(obj.className).split('\s+'));  
  var index = indexOf(array,classStr);  
  if(index != -1){  
    classStr.splice(index,1);  
    obj.className = classStr.join(' ');  
  }  
  return obj;  
}  
//toggleClass函数封装  
function toggleClass(obj,classStr){  
  var array = noRepeat(trim(obj.className).split('\s+'));  
  if(inArray(array,classStr)){  
    removeClass(obj,classStr);  
  }else{  
    addClass(obj,classStr);  
  }  
}  
</script>  
</body>  
</html>    
```


