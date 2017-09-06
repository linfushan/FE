# css hack

##### 兼容范围：

IE:6.0+，FireFox:2.0+，Opera 10.0+，Sarari 3.0+，Chrome

##### 各浏览器hack兼容一览表

| 标记 | IE6 | IE7 | IE8 | FF | Opera | Sarari |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| \[\*+&gt;&lt;\] | ✔ | ✔ | ✘ | ✘ | ✘ | ✘ |
| \_ | ✔ | ✘ | ✘ | ✘ | ✘ | ✘ |
| \9 | ✔ | ✔ | ✔ | ✘ | ✘ | ✘ |
| \0 | ✘ | ✘ | ✔ | ✘ | ✔ | ✘ |
| @media screen and \(-webkit-min-device-pixel-ratio:0\){.bb {}} | ✘ | ✘ | ✘ | ✘ | ✘ | ✔ |
| .bb , x:-moz-any-link, x:default | ✘ | ✔ | ✘ | ✔\(ff3.5及以下\) | ✘ | ✘ |
| @-moz-document url-prefix\(\){.bb{}} | ✘ | ✘ | ✘ | ✔ | ✘ | ✘ |
| @media all and \(min-width: 0px\){.bb {}} | ✘ | ✘ | ✘ | ✔ | ✔ | ✔ |
| \* +html .bb {} | ✘ | ✔ | ✘ | ✘ | ✘ | ✘ |
| 浏览器内核 | Trident | Trident | Trident | Gecko | Presto | Webkit |

（以上**.bb**可更换为其它样式名）

> **注意点：**网上很多资料中常常把`!important`也作为一个hack手段，其实这是一个误区。`!important`常常被我们用来更改样式，而不是兼容hack。造成这个误区的原因是IE6在某些情况下不主动识别!important,以至于常常被人误用做识别IE6的hack。可是，大家注意一下，IE6只是在某些情况下不识别（ie6下，同一个大括号里对同一个样式属性定义，其中一个加important 则important标记是被忽略的，例：`{background:red!important; background:green;}` ie6下解释为背景色green，其它浏览器解释为背景色red；如果这同一个样式在不同大括号里定义，其中一个加important 则important发挥正常作用，例：`div{background:red!important} div{background:green}`，这时所有浏览器统一解释为背景色red。）

#### 实例讲解：

##### Hack应用情境（一）

###### 适用范围：IE:6.0,IE7.0,IE8.0之间的兼容

###### 实例说明：

> 此例中我们使用了渐进识别的方式，从总体中逐渐排除局部。首先，巧妙的使用`\9`这一标记，将IE游览器从所有情况中分离出来。接着，再次使用`+`将**IE8**和**IE7**、**IE6**分离开来，此时，我们的**IE8**已经独立识别。

###### 实例代码：

```css
.bb{
    height:32px;
    background-color:#f1ee18;    /*所有识别*/
    .background-color:#00deff\9; /*IE6、7、8识别*/
    +background-color:#a200ff;   /*IE6、7识别*/
    _background-color:#1e0bd1;   /*IE6识别*/
}
/*一个用于展示的class为bb的div标签*/
< div class ="bb"></ div >
```

---

##### Hack应用情境（二）

###### 适用范围：IE:6.0,IE7.0,IE8.0,Firefox之间的兼容

###### 实例说明：

> 大家很容易的可以看出这是情境（一）的加强版，适用于更广泛的环境。其实情境（一）中也已经做到了把火狐与IE游览器区分开来了，现在我们要做的是把火狐从其它游览器中再次识别出来。大家仔细看下代码，大家会发现其实游览器识别是很简单的。火狐如何识别？对了，IE中对伪类支持不广泛，所以伪类是个不错的途径。`(.yourClass,x:-moz-any-link, x:default)`注意，这个区分伪类往往IE7也能识别，所以最好还需要把IE7单独识别出来，且此方法对ff3.6 已无效，firefox的区分可以使用`@-moz-document url-prefix(){}`

###### 实例代码：

```css
.bb{
    height:32px;
    background-color:#f1ee18;/*所有识别*/
    background-color:#00deff\9; /*IE6、7、8识别*/
    +background-color:#a200ff;/*IE6、7识别*/
    _background-color:#1e0bd1;/*IE6识别*/
}
.bb, x:-moz-any-link, x:default{
    background-color:#00ff00;
}/*IE7 firefox3.5及以下 识别 */ 
@-moz-document url-prefix(){
    .bb{
        background-color:#00ff00;
    }
}/* 仅firefox 识别 */ 
* +html .bb{
    background-color:#a200ff;
}/* 仅IE7 识别 */

/*一个用于展示的class为bb的div标签*/
< div class ="bb"></ div >
```

---

##### Hack应用情境（三）

###### 适用范围：IE:6.0,IE7.0,IE8.0,Firefox,Safari\(Chrome\)之间的兼容

###### 实例说明：

> 我们现在将再次对我们的CSS进行加强了，使其能识别Safari\(Chrome\)游览器。这是基于它们的内核webkit来识别的，用法为`@media screen and (-webkit-min-device-pixel-ratio:0)`

###### 实例代码：

```css
.bb{
    height:32px;
    background-color:#f1ee18;/*所有识别*/
    background-color:#00deff\9; /*IE6、7、8识别*/
    +background-color:#a200ff;/*IE6、7识别*/
    _background-color:#1e0bd1;/*IE6识别*/
}
@media screen and (-webkit-min-device-pixel-ratio:0){
    .bb{
        background-color:#f1ee18
    }
}{} /*safari(Chrome) 有效 */
.bb, x:-moz-any-link, x:default{
    background-color:#00ff00;
}/*IE7 firefox3.5及以下 识别 */ 
@-moz-document url-prefix(){
    .bb{
        background-color:#00ff00;
    }
}/*仅firefox 识别*/ 
* +html .bb{
    background-color:#a200ff;
}/* 仅IE7 识别 */

/*一个用于展示的class为bb的div标签*/
< div class ="bb"></ div >
```

---

##### Hack应用情境（四）

###### 适用范围：IE:6.0+，FireFox:2.0+，Opera 10.0+，Sarari 3.0+，Chrome全兼容

###### 实例说明：

> 实例的具体代码在下面实例代码中已经列出，具体效果如此页面的顶端部分效果，您可以通过不同游览器检测该效果。这次我们基本把所有的主流游览器都兼容了，大家来看下代码。Opera的识别有一部分归功于`\0`标记，这个标记只被**IE8**和**Opera**识别，特殊的标记往往造就的是我们更广泛的hack手段。下例的代码比较完整，大家可以选择参考。

###### 实例代码：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml" lang="gb2312">

    <head>
        <meta http-equiv=Content-Type content="text/html; charset=gb2312" />
        <style type="text/css">
    /***************************************** 各游览器兼容CSS **********************************************/

        .bb {
            height: 32px;
            background-color: #f1ee18;
            /*所有识别*/
            background-color: #00deff\9;
            /*IE6、7、8识别*/
            +background-color: #a200ff;
            /*IE6、7识别*/
            _background-color: #1e0bd1/*IE6识别*/
        }

        @media screen and (-webkit-min-device-pixel-ratio:0) {
            .bb {
                background-color: #f1ee18
            }
        }{}
        /* Safari(Chrome) 有效 */

        @media all and (min-width: 0px) {
            .bb {
                background-color: #f1ee18;
                /*opera and Safari(Chrome) and firefox*/
                background-color: #4cac70\0;
            }
            /* 仅 Opera 有效 */
        }{}

        .bb,
        x:-moz-any-link,
        x:default {
            background-color: #4eff00;
            /*IE7、Firefox3.5及以下 识别 */
        }

        @-moz-document url-prefix() {
            .bb {
                background-color: #4eff00;
                /*仅 Firefox 识别 */
            }
        }

        *+html .bb {
            background-color: #a200ff;
        }
        /* 仅IE7 识别 */
        /* 一般情况下 我们区分IE7 只用 +background-color 配合 _background-color 就行了 如果必须写 .bb, x:-moz-any-link, x:default 这样的代码区分 Firefox3.5及以下 则谨记此写法对IE7也有效，故在其中要再重写一次 +background-color 或者使用 * +html .bb{background-color:blue;} 方法仅对 IE7 有效。可使用 @-moz-document url-prefix(){} 方法独立区分所有 firefox */

        .browsers td {
            width: 8%;
            text-align: center;
            padding: 8px;
        }
    }
    .browsercolor {
        color: #333;
        font-size: 18px;
        font-weight: bold;
    }
    .ie6 {
        background-color: #1e0bd1
    }
    .ie7 {
        background-color: #a200ff
    }
    .ie8 {
        background-color: #00deff
    }
    .firefox {
        background-color: #4eff00
    }
    .opera {
        background-color: #4cac70
    }
    .other {
        background-color: #f1ee18;
    }

    #tipTable td,
    #tipTable th {
        border: 1px solid black;
        width: 56px;
        height: 16px;
        text-align: center;
    }
    #wordTable td {
        margin-left: 8px;
    }
    #firefoxTip {
        display: none;
    }
    #firefoxTip,
    x:-moz-any-link,
    x:default {
        display: block;
        /*IE7 firefox3.5及以下 识别 */

        +display: none
        /*再区分一次IE7*/
    }
    @-moz-document url-prefix() {
        #firefoxTip {
            display: block;
            /*仅 firefox 识别 */
        }
    }
    #ChromeTip {
        display: none;
    }
    @media screen and (-webkit-min-device-pixel-ratio:0) {
        #ChromeTip {
            display: block;
        }
    }{}
    /* safari(Chrome) 有效 */
    @media all and (min-width: 0px) {
        #ChromeTip {
            display: none\0;
        }
        /* 仅 Opera 有效 */
    }{}
        </style>
    </head>

    <body>
        <table class="browsers" width="100%" cellspacing="0" cellpadding="0">
            <tr>
                <td>IE6</td>
                <td></td>
                <td>IE7</td>
                <td></td>
                <td>IE8</td>
                <td></td>
                <td>Firefox</td>
                <td></td>
                <td>Opera</td>
                <td></td>
                <td>Safari(Chrome)</td>
                <td></td>
            </tr>
            <tr class="browsercolor">
                <td class="ie6">IE6</td>
                <td></td>
                <td class="ie7">IE7</td>
                <td></td>
                <td class="ie8">IE8</td>
                <td></td>
                <td class="firefox">Firefox</td>
                <td></td>
                <td class="opera">Opera</td>
                <td></td>
                <td class="other">Safari(Chrome)</td>
                <td></td>
            </tr>
        </table>
        <div class="bb">
            <span style="display:none;display:block\0;display:none\9;">Opera的辨别色是深绿色，Opera游览器很时髦么。</span >
    <span id="firefoxTip">Firefox的辨别色是浅绿色，Firefox是很强大的游览器。</span >
    <span id="ChromeTip">Safari和Chrome的辨别色是金黄色，Safari和Chrome使用的都是Webkit内核</span >
    <!--[if IE 8]>IE8的辨别色是蓝色，新版IE8的功能可是不少呢。<![endif]-->
    <!--[if IE 7]>IE7的辨别色是紫色，IE7还可以凑合着用！<![endif]-->
    <!--[if IE 6]>IE6的辨别色是红色，不过，IE6可是有点落后了！<![endif]-->
</div>
</body>
</html>
```

---

```css
#test{   
    width:300px;   
    height:300px;         
    background-color:blue;      /*firefox*/
    background-color:red\9;     /*all ie*/
    background-color:yellow\0;  /*ie8*/
    +background-color:pink;     /*ie7*/
    _background-color:orange;   /*ie6*/
}  
:root #test {
    background-color:purple\9;
}  /*ie9*/
@media all and (min-width:0px){
    #test {
        background-color:black\0;
    }
}  /*opera*/
@media screen and (-webkit-min-device-pixel-ratio:0){
    #test {
        background-color:gray;
    } 
} /*chrome and safari*/
```

---

> 本文摘自：[CSS hack技巧大全 --作者：吴雷君](http://www.duitang.com/static/csshack.html)



