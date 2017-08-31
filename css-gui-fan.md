# CSS 规范

---

##### CSS文件的分类和引用顺序

按照CSS的性质和用途，将CSS文件分成“公共型样式”、“特殊型样式”、“皮肤型样式”，并以此顺序引用（按需求决定是否添加版本号）。

1. 公共型样式：包括了以下几个部分：“标签的重置和设置默认值”、“统一调用背景图和清除浮动或其他需统一处理的长样式”、“网站通用布局”、“通用模块和其扩展”、“元件和其扩展”、“功能类样式”、“皮肤类样式”。
2. 特殊型样式：当某个栏目或页面的样式与网站整体差异较大或者维护率较高时，可以独立引用一个样式：“特殊的布局、模块和元件及扩展”、“特殊的功能、颜色和背景”，也可以是某个大型控件或模块的独立样式。
3. 皮肤型样式：如果产品需要换肤功能，那么我们需要将颜色、背景等抽离出来放在这里。

```html
<link href="assets/css/global.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/index.css" rel="stylesheet" type="text/css"/>
<link href="assets/css/skin.css" rel="stylesheet" type="text/css"/>
```

##### CSS内部的分类及其顺序

1. 重置（reset）和默认（base）（tags）：消除默认样式和浏览器差异，并设置部分标签的初始样式，以减少后面的重复劳动！你可以根据你的网站需求设置！
2. 统一处理：建议在这个位置统一调用背景图（这里指多个布局或模块或元件共用的图）和清除浮动（这里指通用性较高的布局、模块、元件内的清除）等统一设置处理的样式！
3. 布局（grid）（.g-）：将页面分割为几个大块，通常有头部、主体、主栏、侧栏、尾部等！
4. 模块（module）（.m-）：通常是一个语义化的可以重复使用的较大的整体！比如导航、登录、注册、各种列表、评论、搜索等！
5. 元件（unit）（.u-）：通常是一个不可再分的较为小巧的个体，通常被重复用于各种模块中！比如按钮、输入框、loading、图标等！
6. 功能（function）（.f-）：为方便一些常用样式的使用，我们将这些使用率较高的样式剥离出来，按需使用，通常这些选择器具有固定样式表现，比如清除浮动等！不可滥用！
7. 皮肤（skin）（.s-）：如果你需要把皮肤型的样式抽离出来，通常为文字色、背景色（图）、边框色等，非换肤型网站通常只提取文字色！非换肤型网站不可滥用此类！
8. 状态（.z-）：为状态类样式加入前缀，统一标识，方便识别，她只能组合使用或作为后代出现（.u-ipt.z-dis{}，.m-list li.z-sel{}）

##### 统一语义理解和命名

###### 布局（.g-）

| 语义 | 命名 | 简写 |
| --- | :---: | :--- |
| 文档 | doc | doc |
| 头部 | head | hd |
| 主体 | body | bd |
| 尾部 | foot | ft |
| 主栏 | main | mn |
| 主栏子容器 | mainc | mnc |
| 侧栏 | side | sd |
| 侧栏子容器 | sidec | sdc |
| 盒容器 | wrap/box | wrap/box |

###### 模块（.m-）、元件（.u-）

| 语义 | 命名 | 简写 |
| --- | :---: | :--- |
| 导航 | nav | nav |
| 子导航 | subnav | snav |
| 面包屑 | crumb | crm |
| 菜单 | menu | menu |
| 选项卡 | tab | tab |
| 标题区 | head/title | hd/tt |
| 内容区 | body/content | bd/ct |
| 列表 | list | lst |
| 表格 | table | tb |
| 表单 | form | fm |
| 热点 | hot | hot |
| 排行 | top | top |
| 登录 | login | log |
| 标志 | logo | logo |
| 广告 | advertise | ad |
| 搜索 | search | sch |
| 幻灯 | slide | sld |
| 提示 | tips | tips |
| 帮助 | help | help |
| 新闻 | news | news |
| 下载 | download | dld |
| 注册 | regist | reg |
| 投票 | vote | vote |
| 版权 | copyright | cprt |
| 结果 | result | rst |
| 标题 | title | tt |
| 按钮 | button | btn |
| 输入 | input | ipt |

###### 功能（.f-）

| 语义 | 命名 | 简写 |
| --- | :---: | :--- |
| 浮动清除 | clearboth | cb |
| 向左浮动 | floatleft | fl |
| 向右浮动 | floatright | fr |
| 内联块级 | inlineblock | ib |
| 文本居中 | textaligncenter | tac |
| 文本居右 | textalignright | tar |
| 文本居左 | textalignleft | tal |
| 垂直居中 | verticalalignmiddle | vam |
| 溢出隐藏 | overflowhidden | oh |
| 完全消失 | displaynone | dn |
| 字体大小 | fontsize | fs |
| 字体粗细 | fontweight | fw |

###### 皮肤（.s-）

| 语义 | 命名 | 简写 |
| --- | :---: | :--- |
| 字体颜色 | fontcolor | fc |
| 背景 | background | bg |
| 背景颜色 | backgroundcolor | bgc |
| 背景图片 | backgroundimage | bgi |
| 背景定位 | backgroundposition | bgp |
| 边框颜色 | bordercolor | bdc |

###### 状态（.z-）

| 语义 | 命名 | 简写 |
| --- | :---: | :--- |
| 选中 | selected | sel |
| 当前 | current | crt |
| 显示 | show | show |
| 隐藏 | hide | hide |
| 打开 | open | open |
| 关闭 | close | close |
| 出错 | error | err |
| 不可用 | disabled | dis |

##### 根据属性的重要性按顺序书写

只遵循横向顺序即可，先显示定位布局类属性，后盒模型等自身属性，最后是文本类及修饰类属性

| → | 显示属性 | 自身属性 | 文本属性和其他修饰 |
| --- | :---: | :---: | --- |
| → | display | width | font |
| → | visibility | height | text-align |
| → | position | margin | text-decoration |
| → | float | padding | vertical-align |
| → | clear | border | white-space |
| → | list-style | overflow | color |
| → | top | min-width | background |



