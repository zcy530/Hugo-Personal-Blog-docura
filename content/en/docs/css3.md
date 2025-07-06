---
title: CSS3
slug: CSS3
lastmod: 2025-07-01T00:00:00+00:00
---

- 绝对定位和相对定位
    
    [CSS position 相对定位和绝对定位 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/css-position-static-relative-absolute-fixed.html)
    
    绝对定位：absolute 和 fixed 统称为绝对定位
    
    相对定位：relative
    
    默认值：static
    
    **relative：相对于原来位置移动，元素设置此属性之后仍然处在文档流中，不影响其他元素的布局**
    
    position: relative;相对定位：相对定位是相对于元素在文档中的初始位置——首先它出现在它所在的位置上（即不设置position时的位置，然后通过设置垂直或水平位置，让这个元素“相对于”它的原始起点进行移动；
    
    注意，在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间。因此，移动元素会导致它覆盖其它框。
    
    position: absolute;绝对定位：绝对定位是相对于元素最近的已定位的祖先元素（即是设置了绝对定位或者相对定位的祖先元素）。如果元素没有已定位的祖先元素，那么它的位置则是相对于最初的包含块（body）。
    
    绝对定位本身与文档流无关，因此不占空间，普通文档流中的元素的布局就当绝对定位的元素不存时一样，所以 它们可以覆盖页面上其他的元素，且可以通过z-index属性来控制这些层的对方顺序。
    

### CSS 基础语法

- 选择器(元素、id、类、通用)
    
    **元素选择器**
    
    元素选择器根据元素名称来选择 HTML 元素
    
    ```jsx
    p {
      text-align: center;
      color: red;
    }
    ```
    
    **id选择器**
    
    id 选择器使用 HTML 元素的 id 属性来选择特定元素
    
    元素的 id 在页面中是唯一的，因此 id 选择器用于选择一个唯一的元素！
    
    要选择具有特定 id 的元素，请写一个井号（＃），后跟该元素的 id
    
    ```html
    #para1
    {
        text-align:center;
        color:red;
    }
    ```
    
    **类选择器**
    
    class 选择器用于描述一组元素的样式，class 选择器有别于 id 选择器，class 可以在多个元素中使用
    
    class 选择器在 HTML 中以 class 属性表示，在 CSS 中，类选择器以一个点 **.** 号显示
    
    ```html
    .center 
    { 
        text-align:center; 
    }
    .color 
    { 
        color:#ff0000; 
    }
    ```
    
    你也可以指定特定的 HTML 元素使用 class
    
    在以下实例中, 所有的 p 元素使用 class="center" 让该元素的文本居中
    
    ```html
    p.center {text-align:center;}
    ```
    
    **通用选择器**
    
    通用选择器（*）选择页面上的所有的 HTML 元素
    
    ```jsx
    * {
      text-align: center;
      color: blue;
    }
    ```
    
- CSS 优先级
    
    CSS样式的优先级应该分成四大类
    
    - 第一类`!important`，无论引入方式是什么，选择器是什么，它的优先级都是最高的
    - 第二类引入方式，行内样式的优先级要高于嵌入和外链，嵌入和外链如果使用的选择器相同就看他们在页面中插入的顺序，在后面插入的会覆盖前面的
    - 第三类选择器，选择器优先级：id选择器 > (类选择器 | 伪类选择器 | 属性选择器) > (后代选择器 | 伪元素选择器) > (子选择器 | 相邻选择器) > 通配符选择器
    - 第四类继承样式，是所有样式中优先级比较低的
    - 第五类浏览器默认样式优先级最低
    
    使用!important要谨慎，一定要优先考虑使用样式规则的优先级来解决问题而不是 `!important` ，只有在需要覆盖全站或外部 CSS 的特定页面中使用 `!important` ，永远不要在你的插件中使用 `!important` ，永远不要在全站范围的 CSS 代码中使用 `!important` 
    
    优先级的比较指的是相同的样式属性，不同样式属性优先级比较失效，比如：在设置`max-width`时注意，已经给元素的`max-width`设置了`!important`但是还不生效，很有可能就是被 width 覆盖了 举例：`div`最终的宽度还是`200px` div { max-width: 400px !important; height: 200px;background-color: tomato; width: 200px; }
    
- CSS 插入 html 的方式
    
    插入样式表的方法有三种：
    
    - 外部样式表 (External style sheet)
        
        ```html
        <!DOCTYPE html>
        <html>
            <head>
                <link rel="stylesheet" type="text/css" href="mystyle.css">
            </head>
            <body>
                
                <h1>This is a heading</h1>
                <p>This is a paragraph.</p>
        
            </body>
        </html>
        ```
        
    - 内部样式表 (Internal style sheet)
        
        ```jsx
        <head>
            <style>
                hr {color:sienna;}
                p {margin-left:20px;}
                body {background-image:url("images/back40.gif");}
            </style>
        </head>
        ```
        
    - 内联样式 (Inline style)
        
        ```jsx
        <p style="color:sienna;margin-left:20px">这是一个段落。</p>
        ```
        
    
    一般情况下，优先级如下：
    
    （内联样式）Inline style > （内部样式）Internal style sheet >（外部样式）External style sheet > 浏览器默认样式
    
    ![Untitled](Untitled.png)
    
- Background 背景
    
    [Untitled](Untitled%205929be6a04c346d3a1649ac47db9c9fd.csv)
    
    **背景颜色和透明度**
    
    ```jsx
    div {
      background-color: green;
      opacity: 0.3;
    }
    ```
    
    **背景图片**
    
    ```html
    body {
      background-image: url("paper.gif");
    }
    ```
    
    **背景图片重复** 
    
    默认情况下，`background-image`属性在水平和垂直方向上都重复图像，某些图像应只适合水平或垂直方向上重复，否则它们看起来会很奇怪
    
    只在水平方向重复
    
    ```html
    body {
      background-image: url("gradient_bg.png");
      background-repeat: repeat-x;
    }
    ```
    
    ![Untitled](Untitled%201.png)
    
    不重复
    
    ![Untitled](Untitled%202.png)
    
    **图片位置 position**
    
    ![Untitled](Untitled%203.png)
    
- Color 颜色
    
    ![Untitled](Untitled%204.png)
    
    设置背景颜色
    
    ```html
    <h1 style="background-color:DodgerBlue;">China</h1>
    <p style="background-color:Tomato;">China is a great country!</p>
    ```
    
    设置文本颜色
    
    ```html
    <h1 style="color:Tomato;">China</h1>
    <p style="color:DodgerBlue;">China is a great country!</p>
    ```
    
    设置边框颜色
    
    ```html
    <h1 style="border:2px solid Tomato;">Hello World</h1>
    <h1 style="border:2px solid DodgerBlue;">Hello World</h1>
    ```
    
    ![Untitled](Untitled%205.png)
    
- Text 文本
    
    [Untitled](Untitled%20cd5e8756a39d4081882e88e0f39fb5d8.csv)
    
    **文本颜色**
    
    ![Untitled](Untitled%206.png)
    
    **文本对齐**
    
    ![Untitled](Untitled%207.png)
    
    当 `text-align`属性设置为 "justify" 后，将拉伸每一行，以使每一行具有相等的宽度，并且左右边距是直的（就像在杂志和报纸中）
    
    ![Untitled](Untitled%208.png)
    
    **垂直对齐**
    
    ![Untitled](Untitled%209.png)
    
    **文本方向**
    
    ![Untitled](Untitled%2010.png)
    
    **文字装饰** decoration
    
    `text-decoration` 属性用于设置或删除文本装饰
    
    `text-decoration: none;` 通常用于从链接上删除下划线：
    
    ![Untitled](Untitled%2011.png)
    
    ![Untitled](Untitled%2012.png)
    
    **大小写转换**
    
    ![Untitled](Untitled%2013.png)
    
    **文本缩进 text-indent**
    
    ![Untitled](Untitled%2014.png)
    
    **字母间距 letter-spacing**
    
    ![Untitled](Untitled%2015.png)
    
    **文本阴影 text-shadow**
    
    最简单的用法是只指定水平阴影（2px）和垂直阴影（2px）
    
    ```css
    h1 {
      text-shadow: 2px 2px;
    }
    ```
    
    向阴影添加颜色（红色）
    
    ```css
    h1 {
      text-shadow: 2px 2px red;
    }
    ```
    
    向阴影添加模糊效果（5px）
    
    ```css
    h1 {
      text-shadow: 2px 2px 5px red;
    }
    ```
    
    ![Untitled](Untitled%2016.png)
    
- Border 边框
    
    **边框样式 border-style**
    
    ```css
    p.dotted {border-style: dotted;}
    p.dashed {border-style: dashed;}
    p.solid {border-style: solid;}
    p.double {border-style: double;}
    p.groove {border-style: groove;}
    p.ridge {border-style: ridge;}
    p.inset {border-style: inset;}
    p.outset {border-style: outset;}
    p.none {border-style: none;}
    p.hidden {border-style: hidden;}
    p.mix {border-style: dotted dashed solid double;}
    ```
    
    ![Untitled](Untitled%2017.png)
    
    **边框宽度 border-width**
    
    可以将宽度设置为特定大小（以 px、pt、cm、em 计），也可以使用以下三个预定义值之一：thin、medium 或 thick
    
    `border-width`属性可以设置一到四个值（用于上边框、右边框、下边框和左边框）
    
    ```css
    p.one {
      border-style: solid;
      border-width: 5px 20px; /* 上边框和下边框为 5px，其他边为 20px */
    }
    
    p.two {
      border-style: solid;
      border-width: 20px 5px; /* 上边框和下边框为 20px，其他边为 5px */
    }
    
    p.three {
      border-style: solid;
      border-width: 25px 10px 4px 35px; /* 上边框 25px，右边框 10px，下边框 4px，左边框 35px */
    }
    ```
    
    **边框颜色**
    
    - name - 指定颜色名，比如 "red"
    - HEX - 指定十六进制值，比如 "#ff0000"
    - RGB - 指定 RGB 值，比如 "rgb(255,0,0)"
    - HSL - 指定 HSL 值，比如 "hsl(0, 100%, 50%)"
    - transparent
    
    属性可以设置一到四个值（用于上边框、右边框、下边框和左边框）
    
    ```
    p.one {
      border-style: solid;
      border-color: red green blue yellow; /* 上红、右绿、下蓝、左黄 */
    }
    ```
    
    **简写边框属性**
    
    为了缩减代码，也可以在一个属性中指定所有单独的边框属性
    
    `border` 属性是以下各个边框属性的简写属性：
    
    - `border-width`
    - `border-style`（必需）
    - `border-color`
    
    ```
    p {
      border: 5px solid red;
    }
    
    ```
    
    ![Untitled](Untitled%2018.png)
    
    **圆角边框**
    
    ```css
    p {
      border: 2px solid red;
      border-radius: 5px;
    }
    ```
    
- Margin 外边距
    
    CSS `margin` 属性用于在任何定义的边框之外，为元素周围创建空间。
    
    通过 CSS，您可以完全控制外边距。有一些属性可用于设置元素每侧（上、右、下和左）的外边距
    
    **单独的边**
    
    CSS 拥有用于为元素的每一侧指定外边距的属性：
    
    - `margin-top`
    - `margin-right`
    - `margin-bottom`
    - `margin-left`
    
    所有外边距属性都可以设置以下值：
    
    - auto - 浏览器来计算外边距
    - *length* - 以 px、pt、cm 等单位指定外边距
    - % - 指定以包含元素宽度的百分比计的外边距
    - inherit - 指定应从父元素继承外边距
    
    **简写属性**
    
    ```css
    p {
      margin: 25px 50px 75px 100px;
    }
    ```
    
    - 上外边距是 25px
    - 右外边距是 50px
    - 下外边距是 75px
    - 左外边距是 100px
    
    ```css
    p {
      margin: 25px 50px 75px;
    }
    ```
    
    - 上外边距是 25px
    - 右和左外边距是 50px
    - 下外边距是 75px
    
    ```css
    p {
      margin: 25px 50px;
    }
    ```
    
    - 上和下外边距是 25px
    - 右和左外边距是 50px
    
    ```css
    p {
      margin: 25px;
    }
    ```
    
    - 所有四个外边距都是 25px
    
    **auto 值**
    
    您可以将 margin 属性设置为 `auto`，以使元素在其容器中水平居中
    
    然后，该元素将占据指定的宽度，并且剩余空间将在左右边界之间平均分配
    
    ```css
    div {
      width: 300px;
      margin: auto;
      border: 1px solid red;
    }
    ```
    
    **inherit 值**
    
    ![Untitled](Untitled%2019.png)
    
- Padding 内间距
    
    CSS `padding` 属性用于在任何定义的边界内的元素内容周围生成空间
    
    通过 CSS，您可以完全控制内边距（填充）。有一些属性可以为元素的每一侧（上、右、下和左侧）设置内边距
    
    **单独的边**
    
    CSS 拥有用于为元素的每一侧指定内边距的属性：
    
    - `padding-top`
    - `padding-right`
    - `padding-bottom`
    - `padding-left`
    
    所有内边距属性都可以设置以下值：
    
    - *length* - 以 px、pt、cm 等单位指定内边距
    - % - 指定以包含元素宽度的百分比计的内边距
    - inherit - 指定应从父元素继承内边距
    - 不允许负值
    
    **简写属性**
    
    跟margin一样
    
- height and width 高和宽
    
    `height` 和 `width` 属性可设置如下值：
    
    - `auto` - 默认。浏览器计算高度和宽度
    - `*length*` - 以 px、cm 等定义高度/宽度
    - `%` - 以包含块的百分比定义高度/宽度
    - `initial` - 将高度/宽度设置为默认值
    - `inherit` - 从其父值继承高度/宽度
    

### CSS 中级教程

- Position 定位
    
    规定应用于元素的定位方法的类型，有五个不同的位置值：
    
    - static
    - relative
    - fixed
    - absolute
    - sticky
    
    元素其实是使用 top、bottom、left 和 right 属性定位的。但是，除非首先设置了 position 属性，否则这些属性将不起作用。根据不同的 position 值，它们的工作方式也不同
    
    ### **position: static**
    
    HTML 元素默认情况下的定位方式为 static（静态）
    
    静态定位的元素不受 top、bottom、left 和 right 属性的影响
    
    position: static; 的元素不会以任何特殊方式定位；它始终根据页面的正常流进行定位
    
    ### **position: relative**
    
    相对于其正常位置进行定位
    
    设置相对定位的元素的 top、right、bottom 和 left 属性将导致其偏离其正常位置进行调整。不会对其余内容进行调整来适应元素留下的任何空间
    
    ```html
    div.relative {
      position: relative;
      left: 30px;
      border: 3px solid #73AD21;
    }
    ```
    
    ### **position: fixed**
    
    相对于视口定位的，这意味着即使滚动页面，它也始终位于同一位置。 top、right、bottom 和 left 属性用于定位此元素
    
    固定定位的元素不会在页面中通常应放置的位置上留出空隙
    
    ### **position: absolute**
    
    相对于最近的定位祖先元素进行定位
    
    如果绝对定位的元素没有祖先，它将使用文档主体（body），并随页面滚动一起移动
    
- block/inline 块级元素/行内元素
    
    **块级元素 （block element）**
    
    总是从新行开始，并占据可用的全部宽度（尽可能向左和向右伸展）
    
    - <div>
    - <h1> - <h6>
    - <p>
    - <form>
    - <header>
    - <footer>
    - <section>
    
    **行内元素（inline element）**
    
    内联元素不从新行开始，仅占用所需的宽度
    
    <span>
    
    <a>
    
    <img>
    
- Display 显示和隐藏
    
    display 属性规定是否/如何显示元素：
    
    1. display: none 通常与 JavaScript 一起使用，以隐藏和显示元素，而无需删除和重新创建它们
    2. 如何显示元素：每个 HTML 元素都有一个默认的 display 值，具体取决于它的元素类型。大多数元素的 display 值为 block(块级元素) 或 inline(行内元素)，display 属性可以实现在块级元素和行内元素之间转换
        - 把li变成行内元素
            
            ![Untitled](Untitled%2020.png)
            
        - 把 a 变成块级元素
            
            ![Untitled](Untitled%2021.png)
            
- Overflow 溢出
    
    overflow 属性控制对太大而区域无法容纳的内容的处理方式，指定在元素的内容太大而无法放入指定区域时是剪裁内容还是添加滚动条，overflow 属性仅适用于具有指定高度的块元素。
    
    ![Untitled](Untitled%2022.png)
    
    **overflow 属性可设置以下值：**
    
    - visible：默认。溢出是可见的(visible)，这意味着它不会被裁剪，而是在元素框外渲染
        
        ![Untitled](Untitled%2023.png)
        
    - hidden：溢出被剪裁，其余内容将不可见
        
        ![Untitled](Untitled%2024.png)
        
    - scroll：溢出被剪裁，同时添加滚动条以查看其余内容
        
        ![Untitled](Untitled%2025.png)
        
    - auto：与 scroll 类似，但仅在必要时添加滚动条
        
        ![Untitled](Untitled%2026.png)
        
    
- display:none 和 visibility:hidden 的区别
    - 通过将 display 属性设置为 none可以隐藏元素。该元素将被隐藏，并且页面将显示为好像该元素不在其中，不会占用任何空间
        
        ```tsx
        h1.hidden {
          display: none;
        }
        ```
        
    - visibility:hidden 也可以隐藏元素，但是该元素仍将占用与之前相同的空间。元素将被隐藏，但仍会影响布局
        
        ```tsx
        h1.hidden {
          visibility: hidden;
        }
        ```
        

### 响应式布局

- Flexbox 弹性布局
    
    [CSS Flexbox (w3school.com.cn)](https://www.w3school.com.cn/css/css3_flexbox.asp)
    
    **定义**：弹性框布局模块，可以更轻松地设计灵活的响应式布局结构，而无需使用浮动或定位
    
    **组成**：Flex 容器 + Flex 元素
    
    **使用**：弹性布局中必须有一个 display 属性设置为 flex 的父元素，弹性容器的直接子元素会自动成为弹性项目
    
    ```html
    .flex-container {
      display: flex;
    }
    ```
    
    **示例：**
    
    ![Untitled](Untitled%2027.png)
    
    ```html
    <html>
    <head>
    <style>
    .flex-container {
      display: flex;
      background-color: DodgerBlue;
    }
    
    .flex-container > div {
      background-color: #f1f1f1;
      margin: 10px;
      padding: 20px;
      font-size: 30px;
    }
    </style>
    </head>
    <body>
    
    <div class="flex-container">
      <div>1</div>
      <div>2</div>
      <div>3</div>  
    </div>
    
    </body>
    </html>
    ```
    
    以下是 flex 容器属性：
    
    - flex-direction 定义容器要在哪个方向上堆叠 flex 项目
        
        `column` 值设置垂直堆叠 flex 项目（从上到下）
        
        `column-reverse`值垂直堆叠 flex 项目（但从下到上）
        
        `row` 值水平堆叠 flex 项目（从左到右）
        
        `row-reverse`值水平堆叠 flex 项目（但从右到左）
        
        ```html
        .flex-container {
          display: flex;
          flex-direction: column;
        }
        ```
        
    - flex-wrap 规定是否应该对 flex 项目换行
        
        `wrap` 值规定 flex 项目将在必要时进行换行
        
        `nowrap`值规定将不对 flex 项目换行（默认）
        
        `wrap-reverse`规定如有必要，弹性项目将以相反的顺序换行
        
        ```html
        .flex-container {
          display: flex;
          flex-wrap: wrap;
        }
        ```
        
    - flex-flow 用于同时设置 flex-direction 和 flex-wrap 属性的简写属性
        
        ```html
        .flex-container {
          display: flex;
          flex-flow: row wrap;
        }
        ```
        
    - justify-content 用于对齐 flex 项目
        
        `center` 值将 flex 项目在容器的中心对齐
        
        `flex-start` 值将 flex 项目在容器的开头对齐（默认）
        
        `flex-end` 值将 flex 项目在容器的末端对齐
        
        `space-around`值显示行之前、之间和之后带有空格的 flex 项目
        
        `space-between` 值显示行之间有空格的 flex 项目
        
        ```html
        .flex-container {
          display: flex;
          justify-content: center;
        }
        ```
        
    - align-items 用于垂直对齐 flex 项目
        
        `center`值将 flex 项目在容器中间对齐
        
        `flex-start` 值将 flex 项目在容器顶部对齐
        
        `flex-end` 值将弹性项目在容器底部对齐
        
        `stretch`值拉伸 flex 项目以填充容器（默认）
        
        ```html
        .flex-container {
          display: flex;
          height: 200px;
          align-items: stretch;
        }
        ```
        
        ![Untitled](Untitled%2028.png)
        
    - align-content
- Viewport 可视区域
    
    **作用**
    
    在移动设备上进行网页的重构或开发，更好地让我们的网页适配或响应各种不同分辨率的移动设备
    
    **概念**
    
    移动设备上的viewport就是设备的屏幕上能用来显示我们的网页的那一块区域，在具体一点，就是浏览器上(也可能是一个app中的webview)用来显示网页的那部分区域，但viewport又不局限于浏览器可视区域的大小，它可能比浏览器的可视区域要大，也可能比浏览器的可视区域要小。在默认情况下，一般来讲，移动设备上的viewport都是要大于浏览器可视区域的，这是因为考虑到移动设备的分辨率相对于桌面电脑来说都比较小，所以为了能在移动设备上正常显示那些传统的为桌面浏览器设计的网站，移动设备上的浏览器都会把自己默认的viewport设为980px或1024px（也可能是其它值，这个是由设备自己决定的），但带来的后果就是浏览器会出现横向滚动条，因为浏览器可视区域的宽度是比这个默认的viewport的宽度要小的
    
    **利用meta标签对viewport进行控制**
    
    移动设备默认的viewport是layout viewport，也就是那个比屏幕要宽的viewport，但在进行移动设备网站的开发时，我们需要的是ideal viewport
    
    ```jsx
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    ```
    
    该meta标签的作用是让当前viewport的宽度等于设备的宽度，同时不允许用户手动缩放。也许允不允许用户缩放不同的网站有不同的要求，但让viewport的宽度等于设备的宽度，这个应该是大家都想要的效果，如果你不这样的设定的话，那就会使用那个比屏幕宽的默认viewport，也就是说会出现横向滚动条
    
    meta viewport 有6个属性
    
    [Untitled](Untitled%2020c5b83592724019afd551a01fb161c3.csv)
    
- px 和 rem 和 em 的区别
    
    [(187条消息) css中px、em和rem的区别总结_weixin_30871293的博客-CSDN博客](https://blog.csdn.net/weixin_30871293/article/details/97289333?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-97289333-blog-104593414.pc_relevant_multi_platform_whitelistv4eslandingctr&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-97289333-blog-104593414.pc_relevant_multi_platform_whitelistv4eslandingctr&utm_relevant_index=1)
    
    **px 和 rem 和 em 的区别**
    
    em 和 rem 都是灵活可扩展的单位，由浏览器转换为像素值，取决于设计中的字体大小，如果使用值 1em 或 1rem ，它可以被浏览器转换为从 16px 到 160px 或其他任意值。浏览器使用 1px ，那么 1px 始终显示为完全 1px。
    
    **em 和 rem 的相同点**
    
    使用 em 和 rem 单位可以让我们的设计更加灵活，能够控制元素整体放大缩小，而不是固定大小
    
    **em 和 rem 区别**
    
    区别是浏览器根据谁来转化成 px 值
    
    **rem 单位如何转化为像素值**
    
    当使用 rem 单位，他们转化为像素大小取决于页根元素的字体大小，即 html 元素的字体大小。 根元素字体大小乘以你 rem 值。
    
    例如，根元素的字体大小 16px，10rem 将等同于 160px，即 10 x 16 = 160。
    
    **em 单位如何转换为像素值**
    
    当使用em单位时，像素值将是 em 值乘以使用 em 单位的元素的字体大小。例如，如果一个 div 有 18px 字体大小，10em 将等同于 180px，即 10 × 18 = 180。
    
    **rem使用场景**
    
    一般移动端的UI设计稿的宽度分为375px,和414px两种,但是要想使用一份代码就适配所有屏幕，就必须使用相对单位，这时候使用rem是最好的选择，他可以自动适配所有屏幕，前提是要在html中加上font-size