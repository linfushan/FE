# Sass编译 
[SASS中文网](https://www.sass.hk/)

> 单文件转换编译

```
sass style.scss:style:css
```

> 单文件监听命令

```
sass --watch style.scss:style:css
```

> 文件夹监听命令

```
sass --watch sassFileDirectory:cssFileDirectory
```

> css文件转成sass/scss文件（在线转换工具css2sass）
```
sass-convert style.css style.sass   
sass-convert style.css style.scss
```

####命令行其它选项配置

> 运行命令行帮助文档，可以获得所有的配置选项

```
sass -h
```

> 我们一般常用的有--style，--sourcemap，--debug-info等。

```
sass --watch style.scss:style.css --style compact
sass --watch style.scss:style.css --sourcemap
sass --watch style.scss:style.css --style expanded --sourcemap
sass --watch style.scss:style.css --debug-info
```
> --style表示解析后的css是什么格式，有四种取值分别为：nested，expanded，compact(简单紧凑输出方式)，**compressed**(去掉注释压缩编译)。

> --sourcemap表示开启sourcemap调试。开启sourcemap调试后，会生成一个后缀名为.css.map文件。

> --debug-info表示开启debug信息，升级到3.3.0之后因为sourcemap更高级，这个debug-info就不太用了。

####编译问题

> error：Invalid GBK character "\xE6" 

在cmd里输入一下命令
```
>chcp 65001
```

