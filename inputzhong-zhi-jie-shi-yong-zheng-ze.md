#input中直接使用正则

代码实例：
```js
<h6>只能输入数字和英文 <span>/[^\d]/g</span> </h6>
<input onkeyup="value=value.replace(/[\W]/g,'') " onbeforepaste="clipboardData.setData('text',clipboardData.getData('text').replace(/[\W]/g,''))" ID="Text1" NAME="Text1">
<input onkeyup="value=value.replace(/[^\d]/g,'') " onbeforepaste="clipboardData.setData('text',clipboardData.getData('text').replace(/[^\d]/g,''))" ID="Text2" NAME="Text2">
<h6>只能输入汉字 <span>/[^\u4E00-\u9FA5]/g</span></h6>
<input onkeyup="value=value.replace(/[^\u4E00-\u9FA5]/g,'')" onbeforepaste="clipboardData.setData('text',clipboardData.getData('text').replace(/[^\u4E00-\u9FA5]/g,''))" ID="Text4" NAME="Text4">
```

#####说明
以上时间语法简单说明：
**onbeforepaste**：意思是在用户执行粘贴动作之前
**clipboardData.setData('text', xxx)**：是把xxx的内容复制到剪贴板
**clipboardData.getData('text')**：是读出当前剪贴板里的内容
**.replace(/[ ^\d]/g,'')**：是正则替换，把里面除了数字以外的字符全部都去掉

整个语句的功能是，每当用户执行粘贴操作前，先取出剪贴板的内容字符串，删除不是数字的字符，只保留数字，然后再粘贴，而不是直接粘贴