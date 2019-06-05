# jQuery notes [参考网站](https://www.liaoxuefeng.com/wiki/1022910821149312/1023022609723552)
初次学习jQuery记下的笔记，供日后查询使用。

## 基本选择器
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
var icons = $('[name^=icon]'); // 找出所有name属性值以icon开头的DOM
// 例如: name="icon-1", name="icon-2"
var names = $('[name$=with]'); // 找出所有name属性值以with结尾的DOM
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
--------------------------------------------------
 ## 层次选择器
 ### DOM元素具有层级关系
 ```
 <div class="testing">
    <ul class="lang">
        <li class="lang-javascript">JavaScript</li>
        <li class="lang-python">Python</li>
        <li class="lang-lua">Lua</li>
    </ul>
</div>
```
要选出JavaScript，可以用层级选择器：
```
$('ul.lang li.lang-javascript'); // [<li class="lang-javascript">JavaScript</li>]
$('div.testing li.lang-javascript'); // [<li class="lang-javascript">JavaScript</li>]
```
要选择所有的<li>节点，用：```$('ul.lang li');```
### 子选择器
选择器$('parent>child')类似层级选择器，但是限定了层级关系必须是父子关系，就是<child>节点必须是<parent>节点的直属子节点。
```
$('ul.lang>li.lang-javascript'); // 可以选出[<li class="lang-javascript">JavaScript</li>]
$('div.testing>li.lang-javascript'); // [], 无法选出，因为<div>和<li>不构成父子关系
```
### 过滤器
过滤器一般不单独使用，它通常附加在选择器上，帮助我们更精确地定位元素。观察过滤器的效果：
```
$('ul.lang li'); // 选出JavaScript、Python和Lua 3个节点
$('ul.lang li:first-child'); // 仅选出JavaScript
$('ul.lang li:last-child'); // 仅选出Lua
$('ul.lang li:nth-child(2)'); // 选出第N个元素，N从1开始
$('ul.lang li:nth-child(even)'); // 选出序号为偶数的元素
$('ul.lang li:nth-child(odd)'); // 选出序号为奇数的元素
```
### find() parent() next() prev()
find()方法
```
<ul class="lang">
    <li class="js dy">JavaScript</li>
    <li class="dy">Python</li>
    <li id="swift">Swift</li>
    <li class="dy">Scheme</li>
    <li name="haskell">Haskell</li>
</ul>
```
如果要从当前节点开始向上查找，使用parent()方法：
```
			var a=$('ul.lang');//获得ul
			var b=a.find('#swift');//用find方法获得swift
			var c=b.parent();//用parent方法重回li swift上层节点ul
```
对于位于同一层级的节点，可以通过next()和prev()方法
```
var swift = $('#swift');
swift.next(); // 向下一个得到Scheme
swift.next('[name=haskell]'); // 空的jQuery对象，因为Swift的下一个元素Scheme不符合条件[name=haskell]

swift.prev(); // 向前得到Python
swift.prev('.dy'); // Python，因为Python同时符合过滤器条件.dy
```
### 过滤器filter()
filter()方法可以过滤掉**不符合**选择器条件的节点，即获取filer()括号里要求的节点
```
var langs = $('ul.lang li'); // 拿到所有的li节点:JavaScript, Python, Swift, Scheme和Haskell
var a = langs.filter('.dy'); // 去掉Haskell和swift，拿到JavaScript, Python, Scheme
```
filter()里写函数。
```
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell
langs.filter(function () {
    return this.innerHTML.indexOf('S') === 0; // 返回S开头的节点
}); // 拿到Swift, Scheme
```
**关于indexOf**  
indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置。  
注释：indexOf() 方法对大小写敏感！  
注释：如果要检索的字符串值没有出现，则该方法返回 -1。
```
<script type="text/javascript">
var str="Hello world!"
document.write(str.indexOf("Hello") + "<br />")//0
document.write(str.indexOf("World") + "<br />")//-1表示没出现
document.write(str.indexOf("world"))//6
</script>
```