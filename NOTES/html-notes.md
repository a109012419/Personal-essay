# HTML笔记
用于收录学习html-css时记录下的笔记，供日后查阅
## 单选按钮
``` 
<label><input type="radio" name="indoor-outdoor" checked> Indoor</label>//checked指默认勾选.必须加label作为标签
<label><input type="radio" name="indoor-outdoor"> Outdoor</label>//两个按钮name必须相同，才能达到二选一的功能
```
## 复选按钮
```
<label><input type="checkbox" name="personality" > Loving</label>
<label><input type="checkbox" name="personality"> Lazy</label>
<label><input type="checkbox" name="personality"> Energetic</label>//三个按钮name必须相同
```
## 供用户输入的文本框
```
<input type="text" placeholder="cat photo URL"//placeholder指默认提示 required//required 属性规定必需在提交表单之前填写输入字段
<button type="submit">Submit</button> //提交按钮
<form action="/submit-cat-photo"></form>//form用于向服务器传数据
```
## 超链接
```
<p>Click here for <a href="#">cat photos</a>.</p>//#为超链接网页，必须用<a></a>
```
## style中class优先级
```
.pink-text {
    color: pink;
  }
  .blue-text{
    color:blue;
  }
</style>
<h1 class="pink-text blue-text">Hello World!</h1>
```
**Hello World!是蓝色的,**因为在```<style> ```部分中 class 声明的顺序却非常重要，第二个声明总是比第一个具有优先权。因为``` .blue-text ```是第二个声明，它覆盖了```.pink-text``` 属性。
## important>内联style>id>class
无论在 style 元素 CSS 的哪个位置进行声明，id 声明都会覆盖 class 声明。
而内联样式则会覆盖id声明和class声明。
```
.pink-text {
    color: pink;
  }
<h1 style="color:white" id="orange-text" class="pink-text blue-text">Hello World!</h1>
```
**Hello World!为白色**
```
.pink-text {
    color: pink !important;
  }
<h1 style="color:white" id="orange-text" class="pink-text blue-text">Hello World!</h1>
```
**Hello World!为粉色**