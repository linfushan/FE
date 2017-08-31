# reset

##### 查看默认样式

| html | body | tbody | div |
| :---: | :---: | :---: | :---: |
| ![](/assets/html.png) | ![](/assets/body.png) | ![](/assets/tbody.png) | ![](/assets/div.png) |
| h1 | h2 | h3 | h4 |
| ![](/assets/h1.png) | ![](/assets/h2.png) | ![](/assets/h3.png) | ![](/assets/h4.png) |
| h5 | h6 | p | blockquote |
| ![](/assets/h5.png) | ![](/assets/h6.png) | ![](/assets/p.png) | ![](/assets/blockquote.png) |
| pre | hr | figure | form |
| ![](/assets/pre.png) | ![](/assets/hr.png) | ![](/assets/figure.png) | ![](/assets/form.png) |
| dl | dt | dd | input |
| ![](/assets/dl.png) | ![](/assets/dt.png) | ![](/assets/dd.png) | ![](/assets/input.png) |
| ul | ol | li | button |
| ![](/assets/ul.png) | ![](/assets/ol.png) | ![](/assets/li.png) | ![](/assets/button.png) |
| table | tr | th | td |
| ![](/assets/table.png) | ![](/assets/tr.png) | ![](/assets/th.png) | ![](/assets/td.png) |
| caption | fieldset | legend | textarea |
| ![](/assets/caption.png) | ![](/assets/fieldset.png) | ![](/assets/legend.png) | ![](/assets/textarea.png) |
| menu | img |  | iframe |
| ![](/assets/menu.png) | ![](/assets/img.png) |  | ![](/assets/iframe.png) |

> 从上面的结果可以看出，有margin值的元素有：

`body` `h1` `h2` `h3` `h4` `h5` `h6` `p` `blockquote` `pre` `hr` `figure` `dl` `dd` `ul` `ol` `fieldset` `menu`

> 有padding值的元素有:

`ul` `ol` `button` `th` `td` `fieldset` `legend` `textarea` `menu`

> 有border值的元素有：

`hr` `input` `button` `fieldset` `textarea`

虽然这些都有border,不过个人觉得没有必要进行重置。

##### HTML5新标签针对旧浏览器重置

```css
header,footer,section,article,aside,nav,hgroup,address,figure,figcaption,menu,details{display:block;}
```

##### 其它元素样式重置

######列表
```css
ol,ul{list-style:none;}
```


