# jQuery notes
初次学习jQuery记下的笔记，供日后查询使用。

## 查询
### 按tag查询
```
var ps = $('p'); // 返回所有<p>节点
ps.length; // 计算页面有多少个<p>节点
```
### 按Class查询
```
var a = $('.red'); // 所有节点包含`class="red"`都将返回
// 例如:
// <div class="red">...</div>
// <p class="green red">...</p>

通常很多节点有多个class，我们可以查找同时包含red和green的节点：
var a = $('.red.green'); // 注意没有空格！
// 符合条件的节点：
// <div class="red green">...</div>
// <div class="blue green red">...</div>
```
### 按ID查询
```
// 查找<div id="abc">:
var div = $('#abc');
```
### 按属性查询
```
一个DOM节点除了id和class外还可以有很多属性，很多时候按属性查找会非常方便，比如在一个表单中按属性来查找：
var email = $('[name=email]'); // 找出<??? name="email">
var passwordInput = $('[type=password]'); // 找出<??? type="password">
var a = $('[items="A B"]'); // 找出<??? items="A B">
当属性的值包含空格等特殊字符时，需要用双引号括起来。

按属性查找还可以使用前缀查找或者后缀查找：
var icons = $('[name^=icon]'); // 找出所有name属性值以icon**开头**的DOM
// 例如: name="icon-1", name="icon-2"
var names = $('[name$=with]'); // 找出所有name属性值以with**结尾**的DOM
// 例如: name="startswith", name="endswith"

这个方法尤其适合通过class属性查找，且不受class包含多个名称的影响：
var icons = $('[class^="icon-"]'); // 找出所有class包含至少一个以`icon-`开头的DOM
// 例如: class="icon-clock", class="abc icon-home"
```
### 组合查找
```
组合查找就是把上述简单选择器组合起来使用。如果我们查找$('[name=email]')，很可能把表单外的<div name="email">也找出来，但我们只希望查找<input>，就可以这么写：
var emailInput = $('input[name=email]'); // 不会找出<div name="email">

同样的，根据tag和class来组合查找也很常见：
var tr = $('tr.red'); // 找出<tr class="red ...">...</tr> //tr也是一种tag
```
### 多项选择器
```
多项选择器就是把多个选择器用,组合起来一块选：
$('p,div'); // 把<p>和<div>都选出来
$('p.red,p.green'); // 把<p class="red">和<p class="green">都选出来
```
--------------------------------------------------
### 练习案例
使用jQuery选择器分别选出指定元素：
1. 仅选择JavaScript
2. 仅选择Erlang
3. 选择JavaScript和Erlang
4. 选择所有编程语言
5. 选择名字input
6. 选择邮件和名字input
```
<!-- HTML结构 -->
<div id="test-jquery">
    <p id="para-1" class="color-red">JavaScript</p>
    <p id="para-2" class="color-green">Haskell</p>
    <p class="color-red color-green">Erlang</p>
    <p name="name" class="color-black">Python</p>
    <form class="test-form" target="_blank" action="#0" onsubmit="return false;">
        <legend>注册新用户</legend>
        <fieldset>
            <p><label>名字: <input name="name"></label></p>
            <p><label>邮件: <input name="email"></label></p>
            <p><label>口令: <input name="password" type="password"></label></p>
            <p><button type="submit">注册</button></p>
        </fieldset>
    </form>
</div>
```
**答案：**
```
//仅选择JavaScript
 selected = $('#para-1');
//仅选择Erlang
selected = $('.color-red.color-green');
//选择JavaScript和Erlang
selected = $('#para-1,.color-red.color-green');
//选择所有编程语言
selected = $('[class^=color]');
//选择名字input
selected = $('input[name=name]');
//选择邮件和名字input
selected = $('input[name=name],[name=email]');
```