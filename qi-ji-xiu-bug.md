> 在手机端点击链接或者是按钮的时候，经常会有边框出现，使用一下代码进行消除

```css
* { -webkit-tap-highlight-color: rgba(0,0,0,0); }
```

> 手机端触摸滑动的时候会出现无法滑动或者是卡顿等滑动问题

```html
<script>window.PointerEvent = undefined</script>
<style type="text/css">* { touch-action: none; }</style>
```



