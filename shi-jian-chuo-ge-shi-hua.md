```js
function add0(m){return m<10?'0'+m:m }
function toFormatTime(otime)
{
  //otime是整数，否则要parseInt转换
  var time = new Date(otime);
  var y = time.getFullYear();
  var m = time.getMonth()+1;
  var d = time.getDate();
  var h = time.getHours();
  var mm = time.getMinutes();
  var s = time.getSeconds();
  return y+'-'+add0(m)+'-'+add0(d)+' '+add0(h)+':'+add0(mm)+':'+add0(s);
  console.log(toFormatTime(1403058804));
}
```

> 输出结果：1970-01-17 13:44:18

---

> 获取当前时间戳的办法

第一种方法：

```js
var timestamp = Date.parse(new Date());
//结果：1504056408000
```
第二种方法：
```js
var timestamp = (new Date()).valueOf();
//结果：1504056408935
```
第三种方法：
```js
var timestamp=new Date().getTime();
//结果：1504056408935
```

>第一种：获取的时间戳是把毫秒改成000显示，
第二种和第三种是获取了当前毫秒的时间戳。