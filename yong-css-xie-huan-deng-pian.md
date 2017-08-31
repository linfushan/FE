#用css写幻灯片

```html
<div class="ani"></div>
```

```css
/**css**/
.ani {
    width: 480px;
    height: 320px;
    margin: 50px auto;
    overflow: hidden;
    box-shadow: 0 0 5px rgba(0, 0, 0, 1);
    background-size: cover;
    background-position: center;
    -webkit-animation-name: "loops";
    -webkit-animation-duration: 20s;
    -webkit-animation-iteration-count: infinite;
}

@-webkit-keyframes "loops" {
    0% {
        background: url(https://github.com/linfushan/FE/blob/master/assets/ani1.png) no-repeat;
    }
    25% {
        background: url(https://github.com/linfushan/FE/blob/master/assets/ani2.png) no-repeat;
    }
    50% {
        background: url(https://github.com/linfushan/FE/blob/master/assets/ani3.png) no-repeat;
    }
    75% {
        background: url(https://github.com/linfushan/FE/blob/master/assets/ani4.png) no-repeat;
    }
    100% {
        background: url(https://github.com/linfushan/FE/blob/master/assets/ani1.png) no-repeat;
    }
}
```