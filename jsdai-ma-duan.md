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