# Date

在javascript中用`Date`对象来表示时间和日期

获取当前系统时间：

```js
var now = new Date();
```

| -- | 函数 | 结果 |
| :--- | :--- | :--- |
| 当前时间 | now | Tue Sep 05 2017 17:36:54 GMT+0800 (中国标准时间) |
| 年 | now.getFullYear\(\) | 2017 |
| 月 | now.getMonth\(\) | 8（需要加1,0表示1月份） |
| 日 | now.getDate\(\) | 5 |
| 星期 | now.getDay\(\) | 2 |
| 时 | now.getHours\(\) | 17 |
| 分 | now.getMinutes\(\) | 36 |
| 秒 | now.getSeconds\(\) | 54 |
| 毫秒 | now.getMilliseconds\(\) | 245 |
| 时间戳 | now.getTime\(\) | 1504604214245 |



