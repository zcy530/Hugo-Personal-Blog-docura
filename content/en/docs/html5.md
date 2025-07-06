---
title: HTML5
slug: HTML5
lastmod: 2025-07-01T00:00:00+00:00
---

## html5

- html5语义化
    
    在HTML5出来之前，我们习惯于用div来表示页面的章节或者不同模块，但是div本身是没有语义的。但是现在，HTML5中加入了一些语义化标签，来更清晰的表达文档结构
    
    ```
    <title>      <!--：页面主体内容。-->
    <hn>         <!--：h1~h6，分级标题，<h1> 与 <title> 协调有利于搜索引擎优化。-->
    <ul>         <!--：无序列表。-->
    <li>         <!--：有序列表。-->
    <header>     <!--：页眉通常包括网站标志、主导航、全站链接以及搜索框。-->
    <nav>         <!--：标记导航，仅对文档中重要的链接群使用。-->
    <main>         <!--：页面主要内容，一个页面只能使用一次。如果是web应用，则包围其主要功能。-->
    <article>    <!--：定义外部的内容，其中的内容独立于文档的其余部分。-->
    <section>    <!--：定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。-->
    <aside>         <!--：定义其所处内容之外的内容。如侧栏、文章的一组链接、广告、友情链接、相关产品列表等。-->
    <footer>     <!--：页脚，只有当父级是body时，才是整个页面的页脚。-->
    <small>      <!--：呈现小号字体效果，指定细则，输入免责声明、注解、署名、版权。-->
    <strong>     <!--：和 em 标签一样，用于强调文本，但它强调的程度更强一些。-->
    <em>         <!--：将其中的文本表示为强调的内容，表现为斜体。-->
    <mark>       <!--：使用黄色突出显示部分文本。-->
    <figure>     <!--：规定独立的流内容（图像、图表、照片、代码等等）（默认有40px左右margin）。-->
    <figcaption><!--：定义 figure 元素的标题，应该被置于 figure 元素的第一个或最后一个子元素的位置。-->
    <cite>       <!--：表示所包含的文本对某个参考文献的引用，比如书籍或者杂志的标题。-->
    <blockquoto><!--：定义块引用，块引用拥有它们自己的空间。-->
    <q>          <!--：短的引述（跨浏览器问题，尽量避免使用）。-->
    <time>       <!--：datetime属性遵循特定格式，如果忽略此属性，文本内容必须是合法的日期或者时间格式。-->
    <abbr>       <!--：简称或缩写。-->
    <dfn>       <!--：定义术语元素，与定义必须紧挨着，可以在描述列表dl元素中使用。-->
    <address>    <!--：作者、相关人士或组织的联系信息（电子邮件地址、指向联系信息页的链接）。-->
        <del>        <!--：移除的内容。-->
    <ins>        <!--：添加的内容。-->
    <code>       <!--：标记代码。-->
    <meter>      <!--：定义已知范围或分数值内的标量测量。（Internet Explorer 不支持 meter 标签）-->
    <progress>    <!--：定义运行中的进度（进程）。-->
    ```
    
    语义化优点：
    
    - 易于用户阅读，样式丢失的时候能让页面呈现清晰的结构
    - 有利于SEO，搜索引擎根据标签来确定上下文和各个关键字的权重
    - 方便屏幕阅读器解析，如盲人阅读器根据语义渲染网页
    - 有利于开发和维护，语义化更具可读性，代码更好维护，与CSS3关系更和谐
- html第一行<!DOCTYPE html>
    
    第一行是 **<!DOCTYPE html>**
    
    这个属性会被浏览器识别并使用，但是如果你的页面没有DOCTYPE的声明，那么浏览器按照自己的方式解析渲染页面，那么，在不同的浏览器就会显示不同的样式
    
    <!DOCTYPE> 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令
    
    在 HTML 4.01 中，<!DOCTYPE> 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容，HTML5 不基于 SGML，所以不需要引用 DTD
    
    提示：请始终向 HTML 文档添加 <!DOCTYPE> 声明，这样浏览器才能获知文档类型。
    

# HTML 教程

![Untitled](Untitled.png)

## 基础

```html
<br> 换行
<hr> 水平线
<!-- comment  --> 注释

<h1>这是一个标题</h1>
<h2>这是一个标题</h2>
<h3>这是一个标题</h3>

<p>这是一个段落。</p>
<p>这是另外一个段落。</p>
```

## 元素和属性

如下面的代码：红色的是元素 绿色的是属性

```html
<h1 align="center"> 拥有关于对齐方式的附加信息
<body bgcolor="yellow"> 拥有关于背景颜色的附加信息
<table border="1"> 拥有关于表格边框的附加信息
```

## 格式化文本

[Untitled](Untitled%2054c325a4aedd4d52a6e32e0a41b6423a.csv)

## 链接 a href

```html
1. 网址链接
<a href="[https://www.runoob.com](https://www.runoob.com/)">这是一个链接</a>
<a href="https://www.runoob.com/" target="_blank" rel="noopener noreferrer">访问菜鸟教程!</a>
<a href="http://www.runoob.com/" target="_top">点击这里!</a>
使用 target 属性，你可以定义被链接的文档在何处显示

2. 图片链接
<a href="http://www.runoob.com/html/html-tutorial.html">
<img  border="10" src="smiley.gif" alt="HTML 教程" width="32" height="32">
</a>

<a href="http://www.runoob.com/html/html-tutorial.html">
<img border="0" src="smiley.gif" alt="HTML 教程" width="32" height="32">
</a>

3. 电子邮件链接
<a href="mailto:someone@example.com?Subject=Hello%20again" target="_top">发送邮件</a>
注意:单词之间空格使用 %20 代替，以确保浏览器可以正常显示文本
```

```html
在HTML文档中插入ID
<a id="tips">有用的提示部分</a>  

在HTML文档中创建一个链接到 "有用的提示部分(id="tips"）"
<a href="#tips">访问有用的提示部分</a>

或者，从另一个页面创建一个链接到 "有用的提示部分(id="tips"）"
<a href="https://www.runoob.com/html/html-links.html#tips">
访问有用的提示部分</a>
```

![Untitled](Untitled%201.png)

## 头部 head

<head> 元素包含了所有的头部标签元素。在 <head>元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。可以添加在头部区域的元素标签为: <title>, <style>, <meta>, <link>, <script>, <noscript> 和 <base>

[Untitled](Untitled%200f2a86a12ff947df91b7c581ee3d09be.csv)

```html

1. <link> 标签通常用于链接到样式表
<head>
  <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>

2. 在<style> 元素中你也可以直接添加样式来渲染 HTML 文档
<head>
<style type="text/css">
body {background-color:yellow}
p {color:blue}
</style>
</head>

3. <meta> 标签提供了元数据.元数据也不显示在页面上，但会被浏览器解析。META 元素通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。
<meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
<meta name="description" content="免费 Web & 编程 教程">
<meta name="author" content="Runoob">
<meta http-equiv="refresh" content="30">  每30秒钟刷新当前页面

4. <script>标签用于加载脚本文件，如： JavaScript
```

## 联动 css

CSS 可以通过以下方式添加到HTML中:

- 内联样式- 在HTML元素中使用 "style" **属性**
- 内部样式表 -在HTML文档头部 <head> 区域使用 <style> **元素** 来包含CSS
- 外部引用 - 使用外部 CSS **文件**

```html
1. 内联样式
<p style="color:blue;margin-left:20px;">左边距</p>
<h2 style="background-color:red;">背景颜色</h2>
<h1 style="font-family:verdana;">字体</h1>
<p style="font-family:arial;color:red;font-size:20px;">字体颜色大小</p>
<h1 style="text-align:center;">居中对齐</h1>
<a href="http://www.runoob.com/" style="text-decoration:none;">没有下划线的链接</a>

2. 内联样式表
<head>
<style type="text/css">
body {background-color:yellow;}
p {color:blue;}
</style>
</head>

3. 外部样式文件
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

![Untitled](Untitled%202.png)

![Untitled](Untitled%203.png)

注意：

在HTML 4, 原来支持定义HTML元素样式的标签和属性已被弃用。这些标签将不支持新版本的HTML标签。不建议使用的标签有: <font>, <center>, <strike>，不建议使用的属性: color 和 bgcolor

## 图像 img

```html
1. 插入图像
<img src="/images/logo.png" width="258" height="39" />

2. alt属性：替换文本。alt 属性用来为图像定义一串预备的可替换的文本。在浏览器无法载入图像时，替换文本属性告诉读者她们失去的信息。此时，浏览器将显示这个替代性的文本而不是图像。
<img src="boat.gif" alt="Big Boat">

3. 设置图像的高度与宽度。属性值默认单位为像素
<img src="pulpit.jpg" alt="Pulpit rock" width="304" height="228">
```

## 表格 table

表格由 <table> 标签来定义。每个表格均有若干行（由 <tr> 标签定义），每行被分割为若干单元格（由 <td> 标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等

[Untitled](Untitled%206a13c3f419a149b7ab7fc4320bd8536b.csv)

![Untitled](Untitled%204.png)

## 列表 ul ol dl

```html
1. 无序列表
<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>

<ul style="list-style-type:circle">
 <li>Apples</li>
 <li>Bananas</li>
</ul>

2. 有序列表
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>

<ol type="A">
 <li>Apples</li>
 <li>Bananas</li>
</ol>

3. 自定义列表
自定义列表以 <dl> 标签开始。每个自定义列表项以 <dt> 开始。每个自定义列表项的定义以 <dd> 开始
<dl>
<dt>Coffee</dt>
<dd>- black hot drink</dd>
<dt>Milk</dt>
<dd>- white cold drink</dd>
</dl>
```

[Untitled](Untitled%209873223e0496491aaf4eade44baa8625.csv)

## 布局 div span

[Untitled](Untitled%20f488e046a0d94d938851397a84aaa0e8.csv)

<div> 元素是块级元素，它可用于组合其他 HTML 元素的容器。<div> 元素没有特定的含义。除此之外，由于它属于块级元素，浏览器会在其前后显示折行。如果与 CSS 一同使用，<div> 元素可用于对大的内容块设置样式属性。<div> 元素的另一个常见的用途是文档布局。它取代了使用表格定义布局的老式方法。使用 <table> 元素进行文档布局不是表格的正确用法。<table> 元素的作用是显示表格化的数据

<span> 元素是内联元素，可用作文本的容器。<span> 元素也没有特定的含义。当与 CSS 一同使用时，<span> 元素可用于为部分文本设置样式属性

用div标签布局的例子：

```html
<div id="container" style="width:500px">

  <div id="header" style="background-color:#FFA500;">
    <h1 style="margin-bottom:0;">主要的网页标题</h1></div>

  <div id="menu" style="background-color:#FFD700;height:200px;width:100px;float:left;">
    <b>菜单</b><br>
        HTML<br>
        CSS<br>
        JavaScript</div>

    <div id="content" style="background-color:#EEEEEE;height:200px;width:400px;float:left;">
    内容在这里</div>

    <div id="footer" style="background-color:#FFA500;clear:both;text-align:center;">
    版权 © runoob.com</div>

</div>
```

![Untitled](Untitled%205.png)

用table布局的例子：

下面的例子使用三行两列的表格，第一和最后一行使用 colspan 属性来横跨两列

```html
<table width="500" border="0">
    <tr>
        <td colspan="2" style="background-color:#FFA500;"><h1>主要的网页标题</h1></td>
    </tr>

    <tr>
        <td style="background-color:#FFD700;width:100px;vertical-align:top;"><b>菜单</b><br>HTML<br>CSS<br>JavaScript</td>
        <td style="background-color:#eeeeee;height:200px;width:400px;vertical-align:top;">内容在这里</td>
  </tr>

    <tr>
        <td colspan="2" style="background-color:#FFA500;text-align:center;">版权 © runoob.com</td>
    </tr>
</table>
```

![Untitled](Untitled%206.png)

## 表单和输入 form

HTML 表单表示文档中的一个区域，此区域包含交互控件，将用户收集到的信息发送到 Web 服务器。HTML 表单用于收集用户的输入信息。

[Untitled](Untitled%208a31c2177c8d4c26bad5ce701348866c.csv)

```html
1. 输入框
<form action="">
Username: <input type="text" name="user"><br>
Password: <input type="password" name="password">
</form>

2. 单选和多选框
<form action="">
<input type="radio" name="sex" value="male">男<br>
<input type="radio" name="sex" value="female">女
</form>

<form>
<input type="checkbox" name="vehicle" value="Bike">我喜欢自行车<br>
<input type="checkbox" name="vehicle" value="Car">我喜欢小汽车
</form>

3. 提交 submit
当用户单击确认按钮时，表单的内容会被传送到服务器。表单的动作属性 action 定义了服务端的文件名
action 属性会对接收到的用户输入数据进行相关的处理
<form name="input" action="html_form_action.php" method="get">
Username: <input type="text" name="user">
<input type="submit" value="Submit">
</form>

4. 下拉列表
<form action="">
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat" selected>Fiat</option>
</select>
</form>

5. 文本框
<textarea rows="10" cols="30">
我是一个文本框。
</textarea>
```

![Untitled](Untitled%207.png)

## 框架 iframe

```html
1. 使用
<iframe src="URL"></iframe>

2. 设置高度与宽度
height 和 width 属性用来定义iframe标签的高度与宽度。
属性默认以像素为单位, 但是你可以指定其按比例显示 (如："80%")
<iframe loading="lazy" src="demo_iframe.html" width="200" height="200"></iframe>

3. 移除边框
<iframe src="demo_iframe.htm" frameborder="0"></iframe>

4. 使用 iframe 来显示目标链接页面（没看懂）
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="https://www.runoob.com" target="iframe_a" rel="noopener">RUNOOB.COM</a></p>
```

## 颜色 background-color

HTML 颜色由一个十六进制符号来定义，这个符号由红色、绿色和蓝色的值组成（RGB）。

每种颜色的最小值是0（十六进制：#00），最大值是255（十六进制：#FF）

常用颜色：

[https://www.runoob.com/html/html-colors.html](https://www.runoob.com/html/html-colors.html)

![Untitled](Untitled%208.png)

目前所有浏览器都支持以下颜色名。141个颜色名称是在HTML和CSS颜色规范定义的（17标准颜色，再加124）。下表列出了所有颜色的值，包括十六进制值。

[https://www.runoob.com/html/html-colornames.html](https://www.runoob.com/html/html-colornames.html)

![Untitled](Untitled%209.png)

## Html 脚本 JavaScript

<script>插入脚本的方法

```html
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head>
<body>

<script>
document.write("Hello World!")
</script> 

</body>
</html>
```

<noscript> 标签提供无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。<noscript>元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。只有在浏览器不支持脚本或者禁用脚本时，才会显示 <noscript> 元素中的内容

```html
<script>
document.write("Hello World!")
</script>
<noscript>抱歉，你的浏览器不支持 JavaScript!</noscript>
```

更多JavaScript体验

```html
1. JavaScript事件响应，点击按钮修改文字内容

<p id="demo">JavaScript 可以触发事件，就像按钮点击。</p>

<script>
    function myFunction(){
        document.getElementById("demo").innerHTML="Hello JavaScript!";
    }
</script>

<button type="button" onclick="myFunction()">点击修改文字</button>

2. 点击按钮改变文字颜色

<p id="demo">JavaScript 能改变 HTML 元素的样式</p>

<script>
function myFunction(){
    x=document.getElementById("demo") // 找到元素
    x.style.color="#ff0000";          // 改变样式
}
</script>

<button type="button" onclick="myFunction()">点击修改文字颜色</button>
```

## Html 响应式 web 设计

**什么是响应式 Web 设计？**

- RWD 指的是响应式 Web 设计（Responsive Web Design）
- RWD 能够以可变尺寸传递网页
- RWD 对于平板和移动设备是必需的

第一种方法是自己写

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
<style>
.city {
float: left;
margin: 5px;
padding: 15px;
width: 300px;
height: 300px;
border: 1px solid black;
} 
</style>
</head>

<body>

<h1>W3School Demo</h1>
<h2>Resize this responsive page!</h2>
<br>

<div class="city">
<h2>London</h2>
<p>London is the capital city of England.</p>
<p>It is the most populous city in the United Kingdom,
with a metropolitan area of over 13 million inhabitants.</p>
</div>

<div class="city">
<h2>Paris</h2>
<p>Paris is the capital and most populous city of France.</p>
</div>

<div class="city">
<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
and the most populous metropolitan area in the world.</p>
</div>

</body>
</html>
```

另一个创建响应式设计的方法，是使用现成的 CSS 框架。**Bootstrap** 是最流行的开发响应式 web 的 HTML, CSS, 和 JS 框架。Bootstrap 帮助您开发在任何尺寸都外观出众的站点：显示器、笔记本电脑、平板电脑或手机：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" 
  href="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
</head>

<body>

<div class="container">
<div class="jumbotron">
  <h1>W3School Demo</h1> 
  <p>Resize this responsive page!</p> 
</div>
</div>

<div class="container">
<div class="row">
  <div class="col-md-4">
    <h2>London</h2>
    <p>London is the capital city of England.</p>
    <p>It is the most populous city in the United Kingdom,
    with a metropolitan area of over 13 million inhabitants.</p>
  </div>
  <div class="col-md-4">
    <h2>Paris</h2>
    <p>Paris is the capital and most populous city of France.</p>
  </div>
  <div class="col-md-4">
    <h2>Tokyo</h2>
    <p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
    and the most populous metropolitan area in the world.</p>
  </div>
</div>
</div>

</body>
</html>
```

**总结**

以上已教你如何使用 HTML 创建站点

HTML 是一种在 Web 上使用的通用标记语言。HTML 允许你格式化文本，添加图片，创建链接、输入表单、框架和表格等等，并可将之存为文本文件，浏览器即可读取和显示

HTML 的关键是标签，其作用是指示将出现的内容

# Html5 教程

HTML5是HTML最新的修订版本，HTML5的设计目的是为了在移动设备上支持多媒体

HTML5 中的一些有趣的新改进：

- 完全支持 CSS3
- 拖拽释放(Drag and drop) API
- 用于媒介播放的 <video> 和 <audio> 元素
- 新的语义化标签，比如 article、footer、header、nav、section
- 新的表单控件，比如 calendar、date、time、email、url、search
- 新增选择器 document.querySelector、document.querySelectorAll
- 简单的绘制图形
    - 用于绘画的 <canvas> 元素
    - 使用内联 [SVG](https://www.runoob.com/html/html5-svg.html)。
    - 使用 [CSS3 2D 转换](https://www.runoob.com/css3/css3-2dtransforms.html)、[CSS3 3D 转换](https://www.runoob.com/css3/css3-3dtransforms.html)
- 对本地离线存储的更好的支持
    - 本地存储 localStorage 和 sessionStorage
    - 访问本地文件
    - 本地 SQL 数据
    - 缓存引用
    - Javascript 工作者
    - XHTMLHttpRequest 2
- 多任务 webworker
- 以下的 HTML 4.01 元素在HTML5中已经被删除:
    - 纯表现的元素：basefont、big、center、font、s、strike、tt、u
    - 对可用性产生负面影响的元素：frame、frameset、noframes

注意：

- <!DOCTYPE html> 声明必须位于 HTML5 文档中的第一行
- 对于中文网页需要使用 **<meta charset="utf-8">** 声明编码，否则会出现乱码。有些浏览器(如 360 浏览器)会设置 GBK 为默认编码，则你需要设置为 **<meta charset="gbk">**

## HTML5 新元素

为了更好地处理今天的互联网应用，HTML5添加了很多新元素及功能，比如: 图形的绘制，多媒体内容，更好的页面结构，更好的形式 处理，和几个api拖放元素，定位，包括网页 应用程序缓存，存储，webworker 等。

**<canvas> 新元素**

[Untitled](Untitled%205d98e7335090423798e2963cf0eb6e91.csv)

**新多媒体元素**

[Untitled](Untitled%20df635da3f37046e8ace70393d9300ddc.csv)

**新表单元素**

[Untitled](Untitled%20aa6f9777c4bb44f291b8519c87e88a22.csv)

**新的语义和结构元素**

在HTML5出来之前，我们习惯于用div来表示页面的章节或者不同模块，但是div本身是没有语义的。但是现在，HTML5中加入了一些语义化标签，来更清晰的表达文档结构

```
<title>      <!--：页面主体内容。-->
<hn>         <!--：h1~h6，分级标题，<h1> 与 <title> 协调有利于搜索引擎优化。-->
<ul>         <!--：无序列表。-->
<li>         <!--：有序列表。-->
<header>     <!--：页眉通常包括网站标志、主导航、全站链接以及搜索框。-->
<nav>         <!--：标记导航，仅对文档中重要的链接群使用。-->
<main>         <!--：页面主要内容，一个页面只能使用一次。如果是web应用，则包围其主要功能。-->
<article>    <!--：定义外部的内容，其中的内容独立于文档的其余部分。-->
<section>    <!--：定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。-->
<aside>         <!--：定义其所处内容之外的内容。如侧栏、文章的一组链接、广告、友情链接、相关产品列表等。-->
<footer>     <!--：页脚，只有当父级是body时，才是整个页面的页脚。-->
<small>      <!--：呈现小号字体效果，指定细则，输入免责声明、注解、署名、版权。-->
<strong>     <!--：和 em 标签一样，用于强调文本，但它强调的程度更强一些。-->
<em>         <!--：将其中的文本表示为强调的内容，表现为斜体。-->
<mark>       <!--：使用黄色突出显示部分文本。-->
<figure>     <!--：规定独立的流内容（图像、图表、照片、代码等等）（默认有40px左右margin）。-->
<figcaption><!--：定义 figure 元素的标题，应该被置于 figure 元素的第一个或最后一个子元素的位置。-->
<cite>       <!--：表示所包含的文本对某个参考文献的引用，比如书籍或者杂志的标题。-->
<blockquoto><!--：定义块引用，块引用拥有它们自己的空间。-->
<q>          <!--：短的引述（跨浏览器问题，尽量避免使用）。-->
<time>       <!--：datetime属性遵循特定格式，如果忽略此属性，文本内容必须是合法的日期或者时间格式。-->
<abbr>       <!--：简称或缩写。-->
<dfn>       <!--：定义术语元素，与定义必须紧挨着，可以在描述列表dl元素中使用。-->
<address>    <!--：作者、相关人士或组织的联系信息（电子邮件地址、指向联系信息页的链接）。-->
    <del>        <!--：移除的内容。-->
<ins>        <!--：添加的内容。-->
<code>       <!--：标记代码。-->
<meter>      <!--：定义已知范围或分数值内的标量测量。（Internet Explorer 不支持 meter 标签）-->
<progress>    <!--：定义运行中的进度（进程）。-->
```

语义化优点：

- 易于用户阅读，样式丢失的时候能让页面呈现清晰的结构
- 有利于SEO，搜索引擎根据标签来确定上下文和各个关键字的权重
- 方便屏幕阅读器解析，如盲人阅读器根据语义渲染网页
- 有利于开发和维护，语义化更具可读性，代码更好维护，与CSS3关系更和谐

## Html5 **Canvas**

HTML5 <canvas> 元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成

**创建一个画布**

一个画布在网页中是一个矩形框，通过 <canvas> 元素来绘制

```python
<canvas id="myCanvas" width="200" height="100"
style="border:1px solid #000000;">
</canvas>
```

**使用 JavaScript 来绘制图像**

canvas 元素本身是没有绘图能力的。所有的绘制工作必须在 JavaScript 内部完成：

```python
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");   // 创建 context 对象
ctx.fillStyle="#FF0000";
ctx.fillRect(0,0,150,75);     // 绘制一个红色的矩形
```

上面的 fillRect 方法拥有参数 (0,0,150,75)

意思是：在画布上绘制 150x75 的矩形，从左上角开始 (0,0)

**Canvas 路径**

在Canvas上画线，我们将使用以下两种方法：

- moveTo(*x,y*) 定义线条开始坐标
- lineTo(*x,y*) 定义线条结束坐标

绘制线条

```python
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.moveTo(0,0);
ctx.lineTo(200,100);
ctx.stroke();
```

绘制圆形

```python
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);
ctx.stroke();
```

## Html5 SVG

- SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
- SVG 用于定义用于网络的基于矢量的图形
- SVG 使用 XML 格式定义图形
- SVG 图像在放大或改变尺寸的情况下其图形质量不会有损失
- SVG 是万维网联盟的标准

与其他图像格式相比（比如 JPEG 和 GIF），使用 SVG 的优势在于：

- SVG 图像可通过文本编辑器来创建和修改
- SVG 图像可被搜索、索引、脚本化或压缩
- SVG 是可伸缩的
- SVG 图像可在任何的分辨率下被高质量地打印
- SVG 可在图像质量不下降的情况下被放大

## Html5 video

<video> 元素支持三种视频格式： MP4, WebM, 和 Ogg

[Untitled](Untitled%2075423940a5ca44e59e772b6fba2b9f27.csv)

下面的例子调用了两个方法：play() 和 pause()。它同时使用了两个属性：paused 和 width

```html
<!DOCTYPE html> 
<html> 
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head>
<body> 

<div style="text-align:center"> 
  <button onclick="playPause()">播放/暂停</button> 
  <button onclick="makeBig()">放大</button>
  <button onclick="makeSmall()">缩小</button>
  <button onclick="makeNormal()">普通</button>
  <br> 
  <video id="video1" width="420">
    <source src="mov_bbb.mp4" type="video/mp4">
    <source src="mov_bbb.ogg" type="video/ogg">
    您的浏览器不支持 HTML5 video 标签。
  </video>
</div> 

<script> 
var myVideo=document.getElementById("video1"); 

function playPause() { 
    if (myVideo.paused) 
      myVideo.play(); 
    else 
      myVideo.pause(); 
} 

    function makeBig() { 
    myVideo.width=560; 
} 

    function makeSmall() { 
    myVideo.width=320; 
} 

    function makeNormal() { 
    myVideo.width=420; 
} 
</script> 

</body> 
</html>
```

## Html5 Audio

目前, <audio>元素支持三种音频格式文件: MP3, Wav, 和 Ogg

- control：供添加播放、暂停和音量控件
- 在<audio> 与 </audio> 之间你需要插入浏览器不支持的<audio>元素的提示文本
- <source> 元素可以链接不同的音频文件，浏览器将使用第一个支持的音频文件

```html
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
您的浏览器不支持 audio 元素。
</audio>
```

audio 常用属性

[Untitled](Untitled%202bc187e2a32e45ba85256a27da17c1fb.csv)

audio属性

[Untitled](Untitled%20abf9aa8eaa9647309ee0003d5717e9d1.csv)

常用的控制用的函数：

[Untitled](Untitled%20b89392876eae489f9ba68f10b40de37d.csv)

常用audio的事件：

[Untitled](Untitled%20d7774ef4330d4a89acaf900c07a96ede.csv)

## L**ocalStorage & SessionStorage**

客户端存储数据的两个对象为：

- localStorage - 用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去除
- sessionStorage - 用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据

不管是 localStorage，还是 sessionStorage，可使用的API都相同，常用的有如下几个：

- 保存数据：localStorage.setItem(key,value);
- 读取数据：localStorage.getItem(key);
- 删除单个数据：localStorage.removeItem(key);
- 删除所有数据：localStorage.clear();
- 得到某个索引的key：localStorage.key(index);

**localStorage 对象**

```html
<body>

<div id="result"></div>
<script>
if(typeof(Storage)!=="undefined")
{
  // 存储
  localStorage.setItem("sitename", "菜鸟教程");
  // 查找
  document.getElementById("result").innerHTML = "网站名：" +  localStorage.getItem("sitename");
  localStorage.removeItem("sitename");
}
else
{
  document.getElementById("result").innerHTML="对不起，您的浏览器不支持 web 存储。";
}
</script>

</body>
```

为了简洁易懂，也可以这么写：

```html
// 存储
localStorage.sitename = "菜鸟教程";
// 查找
document.getElementById("result").innerHTML = localStorage.sitename;
```

**sessionStorage 对象**

sessionStorage 方法针对一个 session 进行数据存储。当用户关闭浏览器窗口后，数据会被删除

```html

<script>
function clickCounter()
{
    if(typeof(Storage)!=="undefined")
    {
        if (sessionStorage.clickcount)
        {
            sessionStorage.clickcount=Number(sessionStorage.clickcount)+1;
        }
        else
        {
            sessionStorage.clickcount=1;
        }
        document.getElementById("result").innerHTML="在这个会话中你已经点击了该按钮 " + sessionStorage.clickcount + " 次 ";
    }
    else
    {
        document.getElementById("result").innerHTML="抱歉，您的浏览器不支持 web 存储";
    }
}
</script>

<body>
<p><button onclick="clickCounter()" type="button">点我！</button></p>
<div id="result"></div>
<p>点击该按钮查看计数器的增加。</p>
</body>
```

## **Html5 WebSocket**

WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议

WebSocket 使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输

在 WebSocket API 中，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道。两者之间就直接可以数据互相传送

现在，很多网站为了实现推送技术，所用的技术都是 Ajax 轮询。轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出HTTP请求，然后由服务器返回最新的数据给客户端的浏览器。这种传统的模式带来很明显的缺点，即浏览器需要不断的向服务器发出请求，然而HTTP请求可能包含较长的头部，其中真正有效的数据可能只是很小的一部分，显然这样会浪费很多的带宽等资源

HTML5 定义的 WebSocket 协议，能更好的节省服务器资源和带宽，并且能够更实时地进行通讯