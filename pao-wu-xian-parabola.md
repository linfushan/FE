# parabola

##### 简单粗暴的写了个抛物线运动，主要用于类似购物车载入货物的动作。还不是很完善，没有封装，不过简单易懂。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>抛物线</title>
    <link rel="stylesheet" href="parabola.css">
    <script type="text/javascript" src="parabola.js"></script>
</head>
<body id="parab">
    <div class="parabStart"></div>
    <div class="parabStart" style="left: 100px"></div>
    <div class="parabStart" style="left: 150px"></div>
    <div class="parabStart" style="left: 200px"></div>
    <div class="parabEnd"></div>
</body>
</html>
```

```css
charset "utf-8";
body{
    position: relative;
}
div{
    position: absolute;
    width: 20px;
    height: 20px;
    border-radius: 20px;
}
.moveDot,
.parabStart{
    top: 200px;
    left:60px;
    background-color: aquamarine;
}
.parabEnd{
    top: 280px;
    right:100px;
    background-color: crimson;
}
```

```js
function getClass(oParent, sClass) {
    'use strict';
    var oTag = oParent.getElementsByTagName('*'),
        classArr = [],
        i = 0;
    for (i = 0; i < oTag.length; i++) {
        if (oTag[i].className === sClass) {
            classArr.push(oTag[i]);
        }
    }
    return classArr;
}
function parabolaFunc(that) {
    'use strict';
    var oP = document.getElementById("parab"),
        startEle = that,
        endEle = getClass(oP, "parabEnd")[0],
    //创建一个虚拟的运动对象
        oVm = document.createElement("div");
        oVm.setAttribute("class", "moveDot");
        oP.appendChild(oVm);
    //已知坐标，带入y = a*x*x + b*x + c (a不等于0,a>0开口向下,a<0开口向上)
    //设初始点为原点[0,0],则c=0;
    var x1 = startEle.offsetLeft,
        y1 = startEle.offsetTop,
        x2 = endEle.offsetLeft - x1,
        y2 = endEle.offsetTop - y1,
        a = 0.004,//弧度，值越大弧度越大
    //计算b,c的值
        b = (y2 - a * x2 * x2) / x2,
    //求两点横坐标垂直距离
        x = x2 - x1,
    //设定抛物线的时间，决定运行轨道的时间t=3000ms
        timer = null,
        speed = x / 50,//运动速度
        xDis = 1,       //初始一个大于0的数值
        md = getClass(oP, "moveDot")[0];//获取运动的点

    timer = setInterval(function () {
        xDis += speed;
        var y = a * xDis * xDis + b * xDis;//抛物线函数
        md.style.left = (xDis + x1) + "px";//设置left值
        md.style.top = (y + y1) + "px";    //设置top值
        if (xDis > x2) {//如果横坐标到达终点则结束
            md.style.left = (x1 + x2) + "px";
            md.style.top = (y1 + y2) + "px";
            clearInterval(timer);
            oP.removeChild(md);
        }
    }, 10);

}
window.onload = function () {
    'use strict';
    var oP = document.getElementById("parab"),
        uBtn = getClass(oP, "parabStart"),
        i = 0;
    for(i; i < uBtn.length; i++){
        uBtn[i].onclick = function () {
            parabolaFunc(this);
        };
    }

};
```

#####BUG

> 1.多次连续点击会中断，导致无法再次点击
> 2.由于距离不同，导致运行速度不一致

