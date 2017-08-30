> 防止移动端在输入数字的时候，键盘弹出而挡住输入框。一下代码可直接在键盘弹出的时候将光标所在的输入框移到可视区域。

```js
$(document).on('click','input[type="text"]', function () {
  var target = this;
  setTimeout(function(){
    target.scrollIntoViewIfNeeded();
  },400);
});
```