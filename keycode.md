# keyCode

##### 兼容性

| 属性 | ![](/assets/compatible_chrome.gif) | ![](/assets/compatible_firefox.gif) | ![](/assets/compatible_ie.gif) | ![](/assets/compatible_opera.gif) | ![](/assets/compatible_safari.gif) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| keyCode | Yes | Yes | Yes | Yes | Yes |

##### 获取 Unicode 值

```javascript
var x = event.which||event.keyCode;//// 使用 which 或 keyCode, 这样可支持不同浏览器
alert(x);
```

##### 将 Unicode 值转为字符

```js
var n = String.fromCharCode(65);
alert(n);//A
```

##### 事件绑定

###### onkeypress、onkeydown或onkeyup

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>index</title>
</head>
<body>
    <input id="ipt" type="text">
</body>
<script type="text/javascript">
    var oIpt = document.getElementById("ipt");
    oIpt.onkeyup=function(event){
        var x = event.which||event.keyCode;
        alert(x);
    }
</script>
</html>
```

##### keyCode 值

![](/assets/keycode.png)

