```javascript
/**
 * author:linfs
 * create time:2017-07-25
 */
;(function($){
    $.fn.extend({
        scrollToTop:function(options){
            var defaultSet = {
            btn_str:".fd_fix .back_top",//点击按钮
            dis:100,//滚动距离
            scrollTime:300//滚动过程时间长
        };
        var settings = $.extend(defaultSet,options);
        _top = $(settings.btn_str);
        _top.hide();
        $(window).scroll(function() {
            if ($(window).scrollTop() > settings.dis) {
                _top.fadeIn(400);//当滑动栏向下滑动时，按钮渐现的时间
            } else {
                _top.fadeOut(400);//当页面回到顶部第一屏时，按钮渐隐的时间
            }
        });
        _top.click(function() {console.log(1)
            $('html,body').animate({
                scrollTop: '0px'
            }, settings.scrollTime);
        });
        return this;
        }
    });
})(jQuery);

```
> 调用

```javascript

$(this).scrollToTop();
//或者
$(this).scrollToTop({
    btn_str:".btnName",
    dis:200,
    scrollTime:600
});
```

