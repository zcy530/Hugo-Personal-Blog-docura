---
title: JavaScript
slug: JavaScript
lastmod: 2025-07-01T00:00:00+00:00
---

# **一、初识JS**

## 语言特性

程序语言翻译成机器语言，一种是编译，一种是解释

**编译器**在代码执行之前编译，生成中间代码文件

**解释器**是在运行时进行及时解释，并立即执行

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802170554.png)

运行在客户端的脚本语言，不需要编译，运行过程中由 js 解释器逐行来进行解释并执行

现在也可以基于 node.js 技术进行服务器端的编程

**作用**：表单动态校验，网页特效，服务端开发，桌面程序，app，物联网，游戏开发

**浏览器执行JS简介**：

渲染引擎：解析HTML/CSS

JS引擎：读取网页中的JS代码，对其处理后运行，chorme的V8，执行代码时逐行解释每一句源码

**JS组成**：ECMAScript(语法)，DOM(页面文档对象模型)，BOM(浏览器对象模型)

ECMAScript

## JS 的**三种写法**

行内样式，可读性差在html中编写JS，不方便阅读

```
<body>
    <input type="button" value="点我试试" onclick="alert('hello world')"/>
</body>
```

内嵌式，最常用的

```
<script> alert('s沙漠');
</script>
```

外部JS文件，中间不可以写代码

```
<script src='my.js'></script>
```

注意：JavaScript中都使用单引号

**注释** // (ctrl+/) /**/ (shift+alt+A)

**输入输出语句**

[Untitled](Untitled%2054daeb4b9ddb46758ece45ae8e06c2c3.csv)

注意：prompt取过来的值都是字符型的

## **JS 的变量**

变量是在内存中用于存储数据的容器空间

变量的初始化：1.声明 2. 赋值

```
var age;
var urname = prompt('请输入姓名'); // 在弹出的框中输入 caiyi
console.log(urname); //caiyi
alert(urname); //caiyi
```

声明变量的特殊情况

[Untitled](Untitled%20020931eae7aa4952a56358fdf8e89f23.csv)

**变量命名规范：**

由字母/数字/下划线/美元符号组成

严格区分大小写

不能以数字开头，符号只能美元符号/下划线

不能是关键字/保留字（var for）

变量名必须见名知意/驼峰式命名

# **二、数据类型**

JavaScript是一种弱类型或者说动态语言，不用提前声明变量类型，在运行过程中自动确定

js拥有动态类型，变量的数据类型是可以变化的

## **获取变量类型 typeof**

```
typeof "Bill"                 // 返回 "string"
typeof 3.14                   // 返回 "number"
typeof NaN                    // 返回 "number"
typeof false                  // 返回 "boolean"
typeof [1,2,3,4]              // 返回 "object"
typeof {name:'Bill', age:19}  // 返回 "object"
typeof new Date()             // 返回 "object"
typeof function myFunc(){}    // 返回 "function"
typeof myCar                  // 返回 "undefined" *
typeof null                   // 返回 "object"
```

## **instanceof 判断** prototype 原型链

判断一个构造函数的prototype属性所指向的对象是否在另一个被检测对象的[原型链](https://so.csdn.net/so/search?q=%E5%8E%9F%E5%9E%8B%E9%93%BE&spm=1001.2101.3001.7020)
上

```jsx
obj instanceof F

// obj.proto.proto… => F.prototype，
// 沿着对象obj的原型链查找是否存在对象F.prototype
// 若存在则返回true，若查找到原型链的终点Object.prototype仍未找到，则返回false
```

**例题**

```jsx
function Animal() {};
var a = new Animal();
console.log(a instanceof Animal); // true

function Cat() {}
var c1 = new Cat();
Cat.prototype = a;
var c2 = new Cat();

console.log(c1 instanceof Cat); // false
console.log(c2 instanceof Cat); // true
console.log(c1 instanceof Animal);  // false
console.log(c2 instanceof Animal);  // true
```

![Untitled](Untitled.png)

**手写 instance**

```jsx
function copyInstanceof (source, target) {
    // 基本数据类型以及 null 直接返回 false
    if (!['function', 'object'].includes(typeof source) || source === null) return false
    // getProtypeOf 是 Object 对象自带的一个方法，能够拿到参数的原型对象
    let proto = Object.getPrototypeOf(source)
    while (true) {
        // 查找到尽头，还没找到
        if (proto == null) return false
        // 找到相同的原型对象
        if (proto == target.prototype) return true
        proto = Object.getPrototypeOf(proto)
    }
}

console.log(copyInstanceof("111", String)); // false
console.log(copyInstanceof(new String("111"), String)); // true
console.log(copyInstanceof(Date, Function)); // true
console.log(copyInstanceof(null, Object)); // false
```

**一些容易出错的点**

`Object.create(null)`会造成创建的对象其 `__proto__`指向为空

```jsx
var simpleStr = "This is a simple string"; 
var myString = new String();
var newStr = new String("String created with constructor");
var myDate = new Date();
var myObj = {};
var myNonObj = Object.create(null);

// 返回 false, simpleStr 并不是对象
simpleStr instanceof String;
// 返回 true
myString instanceof String;
// 返回 true
newStr instanceof String;
// 返回 true
myString instanceof Object;
// 返回 true
myObj instanceof Object;
// 返回 true
({}) instanceof Object;
// 返回 false, 一种创建非 Object 实例的对象的方法
myNonObj instanceof Object;
// 返回 false
myString instanceof Date;
// 返回 true
myDate instanceof Date;
// 返回 true
myDate instanceof Object;
// 返回 false
myDate instanceof String;
```

## **constructor 属性确定 object 类型**

`constructor`属性返回所有 JavaScript 变量的构造函数

```jsx
"Bill".constructor                // 返回 function String()  {[native code]}
(3.14).constructor                // 返回 function Number()  {[native code]}
false.constructor                 // 返回 function Boolean() {[native code]}
[1,2,3,4].constructor             // 返回 function Array()   {[native code]}
{name:'Bill',age:19}.constructor  // 返回 function Object()  {[native code]}
new Date().constructor            // 返回 function Date()    {[native code]}
function () {}.constructor        // 返回 function Function(){[native code]}
```

您可以检查 constructor 属性以确定对象是否为数组（包含 `"Array"`一词）

```jsx
function isArray(myArray) {
  return myArray.constructor.toString().indexOf("Array") > -1;
}

function isArray(myArray) {
  return myArray.constructor === Array;
}

function isDate(myDate) {
  return myDate.constructor.toString().indexOf("Date") > -1;
}

function isDate(myDate) {
  return myDate.constructor === Date;
}
```

## **简单数据类型**（Number，Boolean，String，Undefined，Null）

- **number：八进制前加0，十六进制前加0x**
    
    Number.MAX_VALUE
    
    Number.MIN_VALUE
    
    Infinity 无穷大
    
    NaN  isNaN() 判断是非数字
    
- **String：单引号**
    
    长度计算 str.length()
    
    两个引号嵌套，外单内双或外双内单
    
    转义符\n \t \b
    
    字符串拼接用加号 'tianguan' + 'cifu'
    
    字符串 + 其他类型 = 字符串
    
- **Boolean**
    
    true参与加法运算当1，false当0
    
    true +1 = 2
    
    flase + 1 = 1
    
- **undefined 未定义的数据类型**
    
    一个声明后没有被赋值的变量会有一个默认值undefined
    
    var variable = undefined;
    
    variable + 'caiyi' = 'undefinedcaiyi'
    
    variable + 1 = NaN
    
- **Null**
    
    var space = null;
    
    space + 'caiyi' = 'nullpink'
    
    space + 1 = 1
    

## **复杂数据类型**（object，Array，Date，function，set，map）

### Map()

Map 对象存有键值对，其中的键可以是任何数据类型，**能够使用对象作为键**是 Map 的一个重要特性

Map 对象记得键的原始插入顺序

Map 对象具有表示映射大小的属性

[Untitled](Untitled%20a7f3506eacf148e1aef2b0887b8eb100.csv)

[Untitled](Untitled%209a306c98fece4d32b96e46d19021ec17.csv)

创建map

```jsx

// 创建对象
const apples = {name: 'Apples'};
const bananas = {name: 'Bananas'};
const oranges = {name: 'Oranges'};

// 创建新的 Map
const fruits = new Map();

// Add new Elements to the Map
fruits.set(apples, 500);
fruits.set(bananas, 300);
fruits.set(oranges, 200);

// 使用
fruits.get(apples);    // 返回 500
fruits.get("apples");  // 返回 undefined The key is an object (apples), not a string ("apples")
fruits.delete(apples);
fruits.has(apples);
```

### Set()

Set 是唯一值的集合

每个值在 Set 中只能出现一次

一个 Set 可以容纳任何数据类型的任何值

**创建set**

```jsx
// 创建 Set
const letters = new Set();

// 向 Set 添加一些值
letters.add("a");
letters.add("b");
letters.add("c");

// 创建新的 Set
const letters = new Set(["a","b","c"]);
typeof letters; // object
letters instanceof Set;  // true
```

## **数据类型转换**

转换为字符型

```
var num = 1;
str = num.toString();
str = String(num);
str = num + ''; //隐式转换
```

转换为整型

```
var str = '530.9';
num = parseInt(str); //530, 只能得到整数，向下取整，不会四舍五入
num = ParseFloat(str); //得到浮点数
num = Number(str);
num = str - 0;// 用 - * / 做隐式转换
num = str * 1;

console.log(parseInt('3.94')); //3
console.log(parseInt('120px')); //120
console.log(parseInt('rem120px')); //NaN
```

转化为布尔型

```
Boolean(varb);

Boolean('');    //false
Boolean(0);     //false
Boolean(NaN);   //false
Boolean(null);  //false
Boolean(undefined);//false
//除了以上五种情况其他都是true
```

# **三、运算符**

运算符operator也成为操作符

**1. 算数运算符**

浮点数运算会出现误差，尽量不使用

```
console.log(0.1 + 0.2) // 0.30000000000000004
console.log(0.07 * 100) //7.000000000001
console.log(num == 0.3) //false
```

前置递增：先加一，后返回值

后置递增：先返回原值，后自加

```
var num = 10;
++num + 10 //21
num++ + 10 //20

var e = 10;
var f = e++ + ++e; //22
```

2**. 比较运算符**

< >  >= <=

= 赋值（把右边的值给左边）

== 默认转换数据类型（把字符串型数据转换为数字型）

===全等（值和数据类型一模一样）

```
console.log(18 == ‘18’); //true
console.log(18 == ‘18’); //false
```

3**. 逻辑运算符**

与&& 或|| 非!

逻辑与： 表达式1 && 表达式2

两个都是 true 结果才是 true

逻辑或：表达式1 || 表达式2

两个都是 false 结果才是false

**逻辑中断（短路运算）**：

当多个表达式值可以确定结果时就不再继续运算右边表达式的值

# **四、流程控制**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210731120750599.png)

**1. 顺序结构**

按照代码先后顺序，依次执行

**2. 分支结构**

if\if-else；如果if条件表达式结果为真，则执行大括号的代码

```
if () {}
if () {
    ....
} else {
    ....
}
```

```
//case 1
<input type="button" value="if语句案例" onclick="wangba()">
    <script>
        function wangba () {
            var wbage = prompt('how old r u');
            // if((Number(wbage)) >= 18){
            //  alert('come in');
            // }
            if (wbage >= 18) {
                alert('come in');
            }
        }
    </script>
```

```
//case 2 判断闰年
<input type="button" value="判断闰年" onclick="every4Year()">
    <script>
        function every4Year () {
            var urYear = prompt('年份');
            if(uryear % 4 == 0 && uryear % 100 != 0 || uryear % 400 == 0){
                alert('闰年');
            }else{
                alert('平年');
            }
        }
    </script>
```

三元表达式：

`条件表达式 ? 表达式1 : 表达式2 ;`

```
var num = 10;
var result = num > 5 ? 'yes' : 'no';
console.log(result); //表达式是由返回值的
```

switch：

多分支语句 进行匹配 可以多选一

特定值比较合适，有范围的用 if else更合适

```
switch(表达式){
    case value1: 执行语句; break;
    case value2: 执行语句;
    default: 执行语句;break；
```

```
var melon = prompt('水果');
switch(melon){
        case 'apple':
            alert('5.5yuan');
            break;
        case 'banana':
            alert('bananayuan');
            break;
        case '西瓜':
            alert('dont wanna melon');
            break;
        default:
            alert('nothing');
            break;
    }
```

**3. 循环结构**

for循环：

```
var sum = 0;
for(i=1;i<=100;i++){
    sum += i;
}
console.log(sum);
```

双重for循环：

```
var star = '';
for(i=1; i<=10; i++){
    for(j=i; j<=10; j++){
        star += '⭐';
    }
    star += '\n';
}
console.log(star);
```

while循环：

```
var doage = 1;
do{
    console.log(doage);
    doage++;
}while(doage <= 10);
```

断点调试：在浏览器中F12进入开发者模式 -> source -> 找到文件 -> 单击行号打点 -> F11 下一步

continue：跳出本次循环，进入下一次循环

break：跳出整个循环

# **五、数组 Array**

在一个JavaScript数组，你可以放任意不同的数据类型

## **创建数组**

```
var arr = new Array(); // 1.利用new创建空数组
var arry = [];  // 2.利用数组字面量
var arr = new Array(2); // 创建了长度为的为2的空数组
var arr = new Array('caiyi', 100); // 等价于 ['caiyi', 100] 表示2个数组元素
```

## **遍历数组**

```
var arry = ['关羽','张飞','马超','赵云','黄忠','刘备','姜维'];
for (i = 0;i <= 6;i++) {
    console.log(arry[i]);
}
```

数组的长度（元素个数）：arr.length;

## **新增元素**

```
// 1.修改length长度新增数组元素
var arr = [1, 2, 3];
arr.length = 5;
console.log(arr);    //[1,2,3,empty x 2]
console.log(arr[3]); //undefined
console.log(arr[4]); //undefined

// 2.修改数组索引新增元素
var arr = [1, 2, 3];
arr[0] = 0; // replace
arr[3] = 4; // append
console.log(arr);    //[0,2,3,4]
```

## **筛选数组**

可以用 newArr.length 作为插入的下标索引

```
var arr1 = [2,0,6,1,77,0,52,0,25,7];
var newArr = [];
//刚开始 newArry.lengrh 就是0
for (i = 0 ;i < arr1.length; i++) {
    if (arr1[i] >= 10) {
        newwArr[newArr.length] = arr1[i];
    }
}
```

## **冒泡排序**

```
var arr1 = [5,4,3,2,1];
// 比较四趟
for (i = 0; i < arr1.length - 1; i++) {
    //每趟比较次数不同
    for (var j = 0; j < arr1.length - i - 1; j++) {
        // 每个数两两比较
        // if 里的 j 写成了 i ，出错 原因咦想通，花费30分钟
        if (arr1[j] > arr1[j + 1]) {
            var temp = arr1[j];
            arr1[j] = arr1[j + 1];
            arr1[j + 1] = temp;
        }
    }
}
console.log(arr1);
```

## 使用 const 声明数组

2015 年，JavaScript 引入了一个重要的新关键字：`const`

1. 使用 `const` 声明数组已成为一种常见做法，用 `const`声明的数组不能重新赋值：
    
    ```jsx
    const cars = ["Saab", "Volvo", "BMW"];
    cars = ["Toyota", "Volvo", "Audi"];    // ERROR
    ```
    
2. 但可以改变数组的值：
    
    它不定义常量数组，它定义的是对数组的常量引用
    
    因此，我们仍然可以更改const数组的元素
    
    ```jsx
    // 您可以创建常量数组：
    const cars = ["Saab", "Volvo", "BMW"];
    
    // 您可以更改元素：
    cars[0] = "Toyota";
    
    // 您可以添加元素：
    cars.push("Audi");
    ```
    
3. `const` 变量在声明时必须赋值：
    
    意思是：用 `const` 声明的数组必须在声明时进行初始化
    
    ```jsx
    const cars; //error
    cars = ["Saab", "Volvo", "BMW"];
    ```
    

## ⭐const 和 var 的区别

1. 用 `const`声明的数组具有块作用域，用 `var`声明的数组没有块作用域
    
    ```jsx
    var cars = ["Saab", "Volvo", "BMW"];
    {
      var cars = ["Toyota", "Volvo", "BMW"];
    }
    // 此处 cars[0] 为 "Toyota"
    
    const cars = ["Saab", "Volvo", "BMW"];
    {
      const cars = ["Toyota", "Volvo", "BMW"];
    }
    // 此处 cars[0] 为 "Saab"
    ```
    
2. 重新声明数组
    
    ```jsx
    //1. 在程序中的任何位置都允许用 var 重新声明数
    
    var cars = ["Volvo", "BMW"];   // 允许
    var cars = ["Toyota", "BMW"];  // 允许
    cars = ["Volvo", "Saab"];      // 允许
    
    // 2. 不允许在同一作用域，或同一块中将数组重新声明或重新赋值给 const
    
    var cars = ["Volvo", "BMW"];         // 允许
    const cars = ["Volvo", "BMW"];       // 不允许
    {
      var cars = ["Volvo", "BMW"];         // 允许
      const cars = ["Volvo", "BMW"];       // 不允许
    }
    
    // 3. 不允许在同一作用域或同一块中重新声明或重新赋值现有的 const 数组
    const cars = ["Volvo", "BMW"];       // 允许
    const cars = ["Volvo", "BMW"];       // 不允许
    var cars = ["Volvo", "BMW"];         // 不允许
    cars = ["Volvo", "BMW"];             // 不允许
    
    {
      const cars = ["Volvo", "BMW"];     // 允许
      const cars = ["Volvo", "BMW"];     // 不允许
      var cars = ["Volvo", "BMW"];       // 不允许
      cars = ["Volvo", "BMW"];           // 不允许
    }
    
    ```
    

# **六、函数 function**

## 函数的两种**声明（命名和匿名）**

```
// 1.利用函数关键字自定义函数（命名函数）
function fun () {
    ......;
}
// 2.函数表达式（匿名函数）fun是变量名，不是函数名
// 存放在变量中的函数不需要函数名。他们总是使用变量名调用
var fun = function () {};

var fun = function (aru) {
    console.log('我是函数表达式');
    console.log(aru);
}
fun('pink老师');
```

JavaScript 中的 `typeof`运算符会为函数返回 "`function`"

## 箭头函数

```jsx
// ES5
var x = function(x, y) {
  return x * y;
}

// ES6
const x = (x, y) => x * y;
```

箭头函数没有自己的 this。它们不适合定义对象方法

箭头函数未被提升。它们必须在使用前进行定义

使用 const 比使用 var 更安全，因为函数表达式始终是常量值

## **函数的参数**

很随意：

JavaScript 函数定义不会为参数（parameter）规定数据类型

JavaScript 函数不会对所传递的参数（argument）实行类型检查

JavaScript 函数不会检查所接收参数（argument）的数量

[Untitled](Untitled%2067ab9c7b44f5499db3d705ae0b45f34e.csv)

基础传参使用：

```
function cook(aru) { //形参
    console.log(aru);
}
cook('javascript');  //实参
```

传入参数的变化：

参数的改变在函数之外是不可见的

对象属性的改变在函数之外是可见的

## **函数返回值**

只要函数遇到 return 就把后面的结果返回给函数的调用者

```
//求数组中的最大值
function maxfun(arr) { //arr接受一个数组
    var max = arr[0];
    for (i = 1;i < arr.length;i++) {
        if (max < arr[i]) {
            max = arr[i];
        }
    }
    return max;
}
//实参送一个数组过去
//用一个变量来接收 函数的返回结果
var re = maxfun([5, 22, 99, 101, 67, 77]);
```

可使用数组返回多个值 return [num1 + num2, num1 - num2]

函数都有返回值，有 return 则返回对应的值，否则返回 undefined

## 函数的各种调用方法

**全局对象**

当不带拥有者对象调用对象时，`this` 的值成为全局对象

在 web 浏览器中，全局对象就是浏览器对象

本例以 `this` 的值返回这个 window 对象

```jsx
var x = myFunction();            // x 将成为 window 对象

function myFunction() {
   return this;
}
```

**作为方法来调用函数**

在 JavaScript 中，您可以把函数定义为对象方法

下面的例子创建了一个对象（myObject），带有两个属性（firstName 和 lastName），以及一个方法（fullName）

```jsx
var myObject = {
    firstName:"Bill",
    lastName: "Gates",
    fullName: function () {
        return this.firstName + " " + this.lastName;
    }
}
myObject.fullName();         // 将返回 "Bill Gates"
```

```jsx
var myObject = {
    firstName:"Bill",
    lastName: "Gates",
    fullName: function () {
        return this;
    }
}
console.log(myObject.fullName());
```

![Untitled](Untitled%201.png)

**通过函数构造器来调用函数**

```jsx
// 这是函数构造器：
function myFunction(arg1, arg2) {
    this.firstName = arg1;
    this.lastName  = arg2;
}

// 创建了一个新对象：
var x = new myFunction("Bill", "Gates");
x.firstName;
```

## ⭐ **argument 的使用**

当不确定有多少个参数传递时可以使用 arguments 来获取，它是当前函数的一个**内置对象，**所有函数都内置了一个 arguments 对象，存储了所有实参

eg 打印所有的参数

```jsx
function fun () {
    console.log(arguments); //[1,2,3]
    for (var i = 0; i < arguments.length; i++){
        console.log(argument[i]);
    }
}
fun(1,2,3);
```

eg 利用函数求任意个数的最大值

```jsx
x = findMax(1, 123, 500, 115, 44, 88);

function findMax() {
    var i;
    var max = -Infinity;
    for (i = 0; i < arguments.length; i++) {
        if (arguments[i] > max) {
            max = arguments[i];
        }
    }
    return max;
}
```

arguments 是一个伪数组：

1. 具有数组的 length 属性
2. 按照索引的方式进行存储
3. 没有真正数组的一些方法 pop()，push() 等

## ⭐ this 的指向问题

this 表示当前对象的一个引用

但在 JavaScript 中 this 不是固定不变的，它会随着执行环境的改变而改变：

- 在对象方法中，this 表示该方法所属的对象
    
    ```jsx
    var myObject = {
        firstName:"Bill",
        lastName: "Gates",
        fullName: function () {
            return this.firstName + " " + this.lastName;
        }
    }
    myObject.fullName();         // 将返回 "Bill Gates"
    ```
    
    ```jsx
    var myObject = {
        firstName:"Bill",
        lastName: "Gates",
        fullName: function () {
            return this;
        }
    }
    console.log(myObject.fullName());
    ```
    
    ![Untitled](Untitled%201.png)
    
- 如果单独使用，this 表示全局对象
    
    ```html
    var x = this;
    console.log(x);
    ```
    
    ![Untitled](Untitled%202.png)
    
- 在函数中，this 表示全局对象
    
    ```html
    function myFunction() {
        console.log(this);
    }
    myFunction();
    ```
    
    ![Untitled](Untitled%203.png)
    
- 在函数中，在严格模式下，this 是未定义的(undefined)
- 在事件中，this 表示接收事件的元素
    
    ```html
    // 在 HTML 事件处理程序中，this 指的是接收此事件的 HTML 元素：
    <button onclick="this.style.display='none'">
      点击来删除我！
    </button>
    ```
    
- 类似 call() 和 apply() 方法可以将 this 引用到任何对象

## ⭐**JavaScript 预定义方法 Call**

**call()** 和 **apply()** 是预定义的函数方法，两个方法可用于调用函数，两个方法的第一个参数必须是对象本身

`call()`方法是预定义的 JavaScript 方法它可以用来调用所有者对象作为参数的方法，通过 `call()`，您能够使用属于另一个对象的方法，本例调用 person 的 fullName 方法，并用于 person2：

```jsx
var person = {
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
}
var person1 = {
    firstName:"Bill",
    lastName: "Gates",
}
var person2 = {
    firstName:"Steve",
    lastName: "Jobs",
}
person.fullName.call(person1);  // 将返回 "Bill Gates"
person.fullName.call(person2);  // 将返回 "Steve Jobs"
```

带有参数的cal

```jsx
var person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}
var person1 = {
  firstName:"Bill",
  lastName: "Gates"
}
person.fullName.call(person1, "Seattle", "USA");
```

## ⭐**JavaScript 预定义方法 apply**

方法重用：通过 `apply()`方法，您能够编写用于不同对象的方法

`apply()` 方法与 `call()` 方法非常相似，在本例中，`person` 的 `fullName` 方法被***应用***到 `person1`：

```jsx
var person = {
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
}
var person1 = {
    firstName: "Bill",
    lastName: "Gates",
}
person.fullName.apply(person1);  // 将返回 "Bill Gates"
```

带有参数的apply

```jsx
var person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}
var person1 = {
  firstName:"Bill",
  lastName: "Gates"
}
person.fullName.apply(person1, ["Oslo", "Norway"]);
```

区别：

- `call()` 方法分别接受参数
- `apply()` 方法接受数组形式的参数
- 如果要使用数组而不是参数列表，则 `apply()` 方法非常方便

# **七、作用域**

作用域：代码名字（变量）在某个范围内起作用和效果，目的是减少命名冲突

## 全局/函数/块作用域

es6之前分为两大类：**全局作用域**（整个script 标签或者一个单独的js文件），**函数作用域**（也叫局部作用域，函数的内部）es6引入了**块级作用域**

**全局作用域**

在全局作用下使用，在局部变量内没有声明的变量也是全局变量

```
var carName = "porsche";

// 此处的代码可以使用 carName

function myFunction() {
  // 此处的代码也可以使用 carName
}
```

**函数作用域**

在局部作用下（在函数内部），只能在函数内部使用（函数的形参也是局部变量）

特殊情况：在函数内部，没有声明直接赋值的变量也属于全局变量

```html
// 此处的代码不可以使用 carName

function myFunction() {
  var carName = "porsche";
  // code here CAN use carName
}

// 此处的代码不可以使用 carName
```

两个作用域的区别：

全局变量只有在浏览器关闭时才会销毁，比较占内存资源

局部变量当程序执行完毕就会销毁，节约资源

扩展： js 在 es6 中新增块级作用域，花括号包裹即为**块级作用域**（{} if{} for{}）

**块级作用域**

通过 `var` 关键词声明的变量**没有块作用域**，在块 ***{}*** 内声明的变量**可以**从块之外进行访问

（不通过关键词 `var`创建的变量总是全局的，即使它们在函数中创建）

可以使用 `let`关键词声明**拥有块作用域**的变量，在块 ***{}*** 内声明的变量**无法**从块外访问

## let 和 var 的区别

1. 重新声明变量上：
    
    var 在块中重新声明变量也将重新声明块外的变量，let 在块中重新声明变量不会重新声明块外的变量
    
    ```
    var x = 10;
    {
      var x = 6;
    }
    // 此处 x 为 6
    
    var x = 10;
    { 
      let x = 6;
    }
    // 此处 x 为 10
    ```
    
2. 循环作用域
    
    ```jsx
    var i = 7;
    for (var i = 0; i < 10; i++) {
      // 一些语句
    }
    // 此处，i 为 10
    
    let i = 7;
    for (let i = 0; i < 10; i++) {
      // 一些语句
    }
    // 此处 i 为 7
    ```
    
3. 重新声明
    
    ```jsx
    // 1. 允许在程序的任何位置使用 var 重新声明 JavaScript 变量
    var x = 10;
    // 现在，x 为 10
     
    var x = 6;
    // 现在，x 为 6
    
    // 2. 在相同的作用域，或在相同的块中，通过 let重新声明一个 var变量是不允许的
    
    var x = 10;       // 允许
    let x = 6;       // 不允许
    
    {
      var x = 10;   // 允许
      let x = 6;   // 不允许
    }
    
    // 3. 在相同的作用域，或在相同的块中，通过 let 重新声明一个 let 变量是不允许的
    
    let x = 10;       // 允许
    let x = 6;       // 不允许
    
    {
      let x = 10;   // 允许
      let x = 6;   // 不允许
    }
    ```
    

## 嵌套函数的作用域链

内部函数访问外部函数表变量采取链式查找的方式，概括为**就近原则**

在 JavaScript 中，所有函数都有权访问它们“上面”的作用域，JavaScript 支持嵌套函数，嵌套函数可以访问其上的作用域：在本例中，内部函数 `plus()`可以访问父函数中的 `counter`计数器变量

```jsx
function add() {
    var counter = 0;
    function plus() {counter += 1;}
    plus();     
    return counter; 
}
```

```jsx
var num = 10;
function fn () {
    var num = 20;
    function fun () {
        var num = 30;
    }
    function funct () {
        console.log(num); //30
    }
}
```

## ⭐ **JavaScript 闭包**

全局变量能够通过闭包实现局部（私有）

```jsx
var add = (function () {
    var counter = 0;
    return function () {return counter += 1;}
})();

add();
add();
add();
// 计数器目前是 3

// 变量 add 的赋值是自调用函数的返回值
// 这个自调用函数只运行一次。它设置计数器为零（0），并返回函数表达式
// 这样 add 成为了函数。最“精彩的”部分是它能够访问父作用域中的计数器
// 这被称为 JavaScript 闭包。它使函数拥有“私有”变量成为可能
// 计数器被这个匿名函数的作用域保护，并且只能使用 add 函数来修改
// 闭包指的是有权访问父作用域的函数，即使在父函数关闭之后
```

## ⭐ 严格模式

严格模式使我们更容易编写“安全的” JavaScript

严格模式把之前可接受的“坏语法”转变为真实的错误

举例来说，在普通的 JavaScript 中，错打变量名会创建新的全局变量。在严格模式中，此举将抛出错误，这样就不可能意外创建全局变量

在普通 JavaScript 中，如果向不可写属性赋值，开发者不会得到任何错误反馈

在严格模式中，向不可写的、只能读取的、不存在的属性赋值，或者向不存在的变量或对象赋值，将抛出错误

# **八、预解析(变量提升)**

提升（Hoisting）是 JavaScript 将声明移至顶部的默认行为，所以在 JavaScript 中，可以在使用变量之后对其进行声明

```jsx
x = 5; // 把 5 赋值给 x
var x; // 声明 x
```

1. JavaScript 只提升声明，而非初始化
2. js 引擎把 js 中所有的 var 和 function 提升到当前作用域的最前面，用 `let`或 `const`声明的变量和常量不会被提升

**案例引入**

引入1

```
console.log(num); //undefined
var num = 10;
```

引入2

```
fn(); //11
function fn () {
    console.log(11);
}
```

引入3

```
fun(); //error
var fun = function () {
    console.log(22);
}
```

[https://www.notion.so](https://www.notion.so)

## **预解析的作用**

JS 代码是由浏览器中的 JS 解析器来执行的

JS 解析器在运行js代码时分为两步： 预解析和代码执行

**预解析**：js 引擎把 js 中所有的 var 和 function 提升到当前作用域的最前面

**代码执行**： 按照代码书写顺序从上往下执行

① 变量预解析（变量提升）：把所有变量声明提升到当前的作用域最前面，不提升赋值操作

```
console.log(num); //undefined
var num = 10;
//预解析以后相当于执行了以下代码
var num;
console.log(num);
num = 10;
```

```
fun(); // error
var fun = function() {
    console.log(22);
}
//预解析以后相当于执行了以下代码
var fun;
fun();
fun = function() {
    console.log(22);
}
```

② 函数预解析（函数提升）：把所有函数声明提升到当前作用域最前面 不提升函数

```
fn(); //11
function fn () {
    console.log(11);
}
//预解析以后相当于执行了以下代码
function fn () {
    console.log(11);
}
fn(); //11
```

## **预解析案例**

```jsx
var num = 10;
fun();
function fun () {
    console.log(num); //undefined
    var num = 20;
}

//预解析以后相当于执行了以下代码
var num;
function fun () {
    var num;
    console.log(num); //undefined
    num = 20;
}
num = 10;
fun();
```

```jsx
f1();
console.log(c);
console.log(b);
console.log(a);
function f1() {
    var a = b = c = 9;
    //相当于 var a = 9; b = 9; c = 9;
    //b 和 c 直接赋值，没有 var声明，作全局变量
    //集体声明应用逗号隔开 var a = 9, b = 9, c = 9;
    console.log(a); // 9
    console.log(b); // 9
    console.log(c); // 9
}

//预解析以后相当于执行了以下代码
function f1() {
    var a;
    a = b = c = 9;
    console.log(a); // 9
    console.log(b); // 9
    console.log(c); // 9
}
f1();
console.log(c); //9
console.log(b); //9
console.log(a); //报错，因为b、c是全局变量，a是局部变量
```

# **九、对象**

对象是一组无序的相关**属性和方法**的集合

**属性** ：事物的特征，在对象中用属性来表示（常用名词）

**方法**： 事物的行为，在对象中用方法来表示（常用动词）

在 JavaScript 中，几乎“所有事物”都是对象

- 布尔是对象（如果用 ***new*** 关键词定义）
- 数字是对象（如果用 ***new*** 关键词定义）
- 字符串是对象（如果用 ***new*** 关键词定义）
- 日期永远都是对象
- 算术永远都是对象
- 正则表达式永远都是对象
- 数组永远都是对象
- 函数永远都是对象
- 对象永远都是对象

所有 JavaScript 值，除了原始值，都是对象

[https://eastmoney.ceping.com/Login/Elink?elink=Sxrbt5DeQNCYrh4wZn97zqVNGdIV3eCiU7yJIMymZRAH88RLQdq7sF1Y4RJq12w3&v=1](https://eastmoney.ceping.com/Login/Elink?elink=Sxrbt5DeQNCYrh4wZn97zqVNGdIV3eCiU7yJIMymZRAH88RLQdq7sF1Y4RJq12w3&v=1)

## **创建对象的三种方式**

1. 利用字面量 {}
    
    ```
    var obj = {}; // 创建了一个空的对象
    
    var obj = {
        uname: 'zhangcaiyi',
        age: 18,
        sex: '女',
        sayHi: function () {
            console.log('Hi!');
        }
    }
    // 属性或方法采用键值对的形式 属性名: 值
    // 多个属性间用','隔开
    // 方法':'后面跟的是一个匿名函数
    ```
    
2. 利用 new Object
    
    ```
    var obj = new Object(); // 创建了一个空对象
    
    obj.uname = 'zhangcaiyi';
    obj.age = 18;
    obj.sex = '女';
    obj.sayHi = function () {
        console.log('Hi');
    }
    // 利用等号 = 赋值的方法添加对象的属性和方法
    // 每个属性和方法之间用';'结束
    ```
    
3. 利用构造函数
    
    利用函数的方法，重复相同的代码，把对象中的**相同属性和方法**抽离出来封装
    
    ```
    function SuperStar (uname, age, sex) {
        this.name = uname;
        this.age = age;
        this.sex = sex;
        this.sing = function(song) {
            console.log(song);
        }
    }
    var gd = new SuperStar('GD', 30, 'man'); // 调用构造函数 返回的是一个对象
    var jay = new SuperStar('Jay',40,'man');
    console.log(typeof gd); //object
    jay.sing('稻香');
    
    // 构造函数名首字母要大写
    // 构造函数不需要 return 就可以返回结果
    // 调用构造函数必须使用 new
    ```
    

使用对象：

```
console.log(obj.uname);
console.log(obj['uname']);
obj.sayHi();
```

**概念辨析**

1. 变量/属性/方法/函数辨析：
    
    变量：单独声明并赋值，使用时直接写变量名
    
    属性：在对象里不需要声明 使用时必须是 对象.属性
    
    函数：单独声明并且调用 函数名() 单独存在
    
    方法：在对象里调用时 对象.方法
    
2. 构造函数和对象辨析：
    
    构造函数：如Star()，抽象了对象的公共部分封装，封装到函数里面，泛指一大类（class）
    
    对象：如new Star()，特指一个具体的事物，利用构造函数创建对象的过程也称为**对象的实例化**
    

## **new关键字**

new 在执行函数时会做四件事

- 在内存中创建一个新的空对象
- 让 this 指向这个对象
- 执行构造函数内的代码，给新对象添加属性和方法
- 返回这个新对象（所以构造函数里不需要 return）

## **遍历对象 for in**

```
var obj = {
    name: 'dora',
    age: 18,
    sex: 'woman',
    fn: function (){}
}
// for (变量 in 对象)
for (var k in obj) {
    console.log(k);      // 输出得到属性名name, age, sex
    console.log(obj[k]); // obj[k] 得到属性值，k不加引号噢
    //按顺序依次输出：属性名和属性值
}
```

## 对象赋值 x = person

对象是易变的：它们通过引用来寻址，而非值

如果 person 是一个对象，下面的语句不会创建 person 的副本

```jsx
var x = person;  // 这不会创建 person 的副本
```

对象 x 并非 person 的副本。它就是 person，**x 和 person 是同一个对象**，对 x 的任何改变都将改变 person，因为 x 和 person 是相同的对象

```jsx
var person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"}
 
var x = person;
x.age = 10;           // 这将同时改变 both x.age 和 person.age
```

## 显示对象 **Object.values() 和 JSON.stringify()**

转化为数组

```jsx
const person = {
  name: "Bill",
  age: 19,
  city: "Seattle"
};

const myArray = Object.values(person);
console.log(myArray);
```

![Untitled](Untitled%204.png)

转化为字符串

```jsx
const person = {
  name: "Bill",
  age: 19,
  city: "Seattle"
};

let myString = JSON.stringify(person);
console.log(myString);
```

![Untitled](Untitled%205.png)

## 对象构造器

```jsx
function Person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
var myFather = new Person("Bill", "Gates", 62, "blue");
var myMother = new Person("Steve", "Jobs", 56, "green");
```

您***无法***为已有的对象构造器添加新属性

```html
Person.nationality = "English";
```

如需向构造器添加一个新属性，则必须把它添加到构造器函数

```html
function Person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
    this.nationality = "English";
}
```

## ⭐对象原型 prototype

**原型继承**

所有 JavaScript 对象都从原型继承属性和方法，日期对象继承自 Date.prototype。数组对象继承自 Array.prototype。Person 对象继承自 Person.prototype

Object.prototype 位于原型继承链的顶端：日期对象、数组对象和 Person 对象都继承自 Object.prototype

**使用 `prototype` 属性**

JavaScript prototype 属性允许您为对象构造器添加新属性：

```jsx
function Person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
Person.prototype.nationality = "English";
```

JavaScript prototype 属性也允许您为对象构造器添加新方法

```jsx
function Person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
Person.prototype.name = function() {
    return this.firstName + " " + this.lastName;
};
```

请只修改***您自己***的原型，绝不要修改标准 JavaScript 对象的原型

# 十一、类 class

ECMAScript 2015，也称为 ES6，引入了 JavaScript 类

NOTE：JavaScript 类不是对象，它是 JavaScript 对象的**模板**

## 创建和使用

```jsx
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
  age() {
    let date = new Date();
    return date.getFullYear() - this.year;
  }
    calculateAge(x) {
        return x - this.year;
      }
}
```

```jsx
let myCar1 = new Car("Ford", 2014);
let myCar2 = new Car("Audi", 2019);
console.log(myCar1.age());   // 8
console.log(myCar1.age(year));   // 8
```

## 严格模式

在“严格模式”下，如果您使用变量而不声明它，会得到错误

```jsx
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
  age() {
    // date = new Date();  // This will not work
    let date = new Date(); // This will work
    return date.getFullYear() - this.year;
  }
}
```

## 类继承

如需创建类继承，请使用 `extends`关键字

# **十、内置对象**

js 中对象分为： 自定义对象、内置对象、浏览器对象

学会使用MDN查询文档：[https://developer.mozilla.org/zh-CN/](https://developer.mozilla.org/zh-CN/)

### **MATH**

不是一个构造函数，所以不需要 new 来调用，而是直接使用里面的方法和属性

```
Math.PI                 // 圆周率
Math.floor()            // 向下取整
Math.ceil()             // 向上取整
Math.round()            // 四舍五入版 就近取整  -3.5 结果为 -3
Math.abs()              // 绝对值
Math.max()              // 最大值
Math.min()              // 最小值
```

```
//max方法说明
console.log(Math.PI);           //一个属性 圆周率
console.log(Math.max(1, 99,3)); // 99
console.log(Math.max(-1, -10)); // -1
console.log(Math.max(1, 99, 'pink')); // NaN 有字符串或其他类型数据
console.log(Math.max());              // -Infinity 空值返回负无穷
```

随机数方法random()

Math.random() 返回一个 [0,1) 随机的小数

Math.getRandomInt() 返回一个 [min, max) 的随机整数

```
function getRandomInt (min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor( Math.random() * (max - min) ) + min;
}
```

Math.getRandomIntInclusive() 返回一个 [min, max] 的随机整数，包含 min 和 max

```
function getRandomIntInclusive (min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor( Math.random() * (max - min + 1) ) + min;
}
// 随机点名
var arr = ['张三', '张三丰', '李四', '李思思'];
console.log(arr[getRandomIntInclusive(0,3)]);
```

### **DATE**

跟math不一样的是，date是一个**构造函数**，必须用new来调用创建日期对象

1. 使用 Date 如果**没有参数**，则返回当前系统的当前时间

```
var date = new Date();
console.log(date);
//Sun Aug 01 2021 17:10:18 GMT+0800 (中国标准时间)
```

1. 参数的常用写法：
    
    数字型 2020, 04, 05  数字用逗号隔开
    
    字符串型 '2020-04-05 16:34:59' 日期用横线隔开，时间用冒号隔开
    

```
var date1 = new Date(2020, 4, 5);
console.log(date1);
// Fri May 05 2020 00:00:00 GMT+0800 (中国标准时间)
// 注意：返回的是5月，而不是4月

var date2 = new Date('2020-04-05 16:34');
console.log(date2);
// Sun Apr 05 2020 16:34:00 GMT+0800 (中国标准时间)
```

1. 格式化日期：

[Untitled](Untitled%2045656f9f4bd6448486758d79b372b08e.csv)

函数使用的举例：

```
var date3 = new Date();
console.log(date3.getFullYear()); // 返回当前日期的年
console.log(date3.getMonth() + 1); // 月份 0-11
```

格式化时分秒的例子：

```
function getTime() {
    var time = new Date();
    var h = time.getHours();
    h = h < 10 ? '0' + h : h;
    var m = time.getMinutes();
    m = m < 10 ? '0' + m : m;
    var s = time.getSeconds();
    s = s < 10 ? '0' + s : s;
    return h + ':' + m + ':' + s ;
}
console.log(getTime());
```

获取日期的总的毫秒数（时间戳）：

从1970年1月1日开始起到现在的毫秒数

```
// 1. 通过 valueOf() getTime()
var date = new Date();
console.log(date.valueOf());
console.log(date.getTime());

// 2. 简单的写法 （最常用）
var date1 = +new Date(); // +new Date() 返回的就是总毫秒数
console.log(date1);

// 3. h5 新增的 获得总的毫秒数
console.log(Date.now());
```

1. 倒计时：

核心算法：输入时间减去现在的时间即倒计时，但不能拿时分秒相减，用时间戳来完成

把剩余时间转换为天，时，分，秒

公式如下：

```
d = parseInt(总秒数/60/60/24); // 计算天数
h = parseInt(总秒数/60/60%24);     // 计算小时
m = parseInt(总秒数/60%60);        // 计算分数
s = parseInt(总秒数%60);          // 计算当前秒数
```

```
// 下面转换时间
function countDown (time) {
    var nowTime = +new Date();       // 获取当前时间
    var inputTime = +new Date(time); // 获取输入的时间
    var times = (inputTime - nowTime) / 1000; // 剩余时间 秒数

    var d = parseInt(times/60/60/24);
    d = d < 10 ? '0' + d : d;
    var h = parseInt(times/60/60%24);
    h = h < 10 ? '0' + h : h;
    var m = parseInt(times/60%60);
    m = m < 10 ? '0' + m : m;
    var s = parseInt(times%60);
    s = s < 10 ? '0' + s : s;

    return d + '天' + h + '小时' + m + '分钟' + s + '秒' ;

}
console.log(countDown('2020-4-7 16:00:00'));
```

### **ARRAY**

检测是否为数组的两种方式：

```
// 1.instanceof
var arr = [];
consolo.log(arr instanceof Array); //true
var obj = {};
consolo.log(obj instanceof Array); //false

// 2.Array.isArray()
consolo.log(Array.isArray(arr));  //true
consolo.log(Array.isArray(obj));  //false
```

添加删除数组元素：

[Untitled](Untitled%20ecebff385a8245e4bcb2b0b392d14ac5.csv)

```
var arr = [1, 2, 3];
arr.push(4,5); //[1,2,3,4,5]
console.log(arr.push(4,5,6)); //5
arr.unshift(0) //[0,1,2,3,4,5]
```

数组排序：

```
arr.reverse();  //翻转数组
arr.sort();     //冒泡排序，把数字当成字符串排序，结果[1,13,4,7,77]
arr.sort(function(a,b) {
    return a-b; //升序排列 [1,4,7,13,77]
})
```

返回数组索引号：

[Untitled](Untitled%20aefe2261cef245b4bba70bf5dd764241.csv)

数组去重：

核心算法： 遍历旧数组，拿着旧数组去查询新数组，该元素没出现过则添加，否则不添加

利用 新数组.indexOf(数组元素) 返回 -1，则表示不重复

```
function unique(arr) {
    var newArr = [];
    for (var i = 0; i < arr.length; i++) {
        if (newArr.indexOf(arr[i]) === -1) {
            newArr.push(arr[i]);
        }
    }
    return newArr; // 遍历完毕后返回
}
```

数组转换为字符串：

```
arr.toString();
arr.join('分割符');

//example
var arr = [1,2,3];
console.log(arr.toString()); //1,2,3
var arr = ['green','pink','blue'];
console.log(arr.join('-')); //green-pink-blue
```

其他常用函数：

[Untitled](Untitled%20f769959847284a268fbd777fee8a7551.csv)

```
var uniq1 = [1, 2, 3, 4, 5];
var uniq2 = [6, 7, 8, 9, 0];
var uniq3 = [];
var uniq4 = [6, 7, 8, 9, 0];
console.log(uniq3.concat(uniq1, uniq2)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
console.log(uniq1.slice(1,3)); // [2,3] 默认不包括结束位置的元素
console.log(uniq1); // 不变 [1, 2, 3, 4, 5]
console.log('uniq4+' + uniq4); // uniq4+6,7,8,9,0
console.log(uniq4.splice(2,2)); //[8, 9]
console.log('splice后的' + uniq4); // splice后的6,7,0
```

### **STRING**

**基本包装类型**：把简单数据类型包装成为复杂数据类型，这样基本数据类型就有了属性和方法

js 提供了三种基本包装类型：String，Number，Boolean

```
var str = ‘uniq’;
console.log(str.length); // 基本数据类型本无属性和方法
//但以上代码可执行是因为 JS 会把基本数据类型包装为复杂数据类型 执行过程如下：

// 1. 生成临时变量，把简单数据类型包装为复杂数据类型
var temp = new String(‘uniq’);
// 2. 赋值给我们声明的字符变量
str = temp;
// 3.销毁临时变量
temp = null;
```

**字符串的不可变性**：

指的是里面的值不变，实质改变的是地址 在内存中开辟了新的存储空间（指针改变了）

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802170748.png)

- 当重新给 str 赋值时， 常量 ‘andy’ 不会被修改，但依然在内存中
- 重新给字符串赋值，会重新在内存中开辟空间 'red' ，这就是字符串的不可变
- 由于字符串的不可变，在大量拼接字符串时就会产生效率问题

**返回字符的位置：**

```
str.indexOf(x,a,b); //从a的索引号开始查找x，到b（不包括）
str.lastIndexOf(x);
```

例子：查找 ’abcosidfnoiojisoo' 中所有o出现的位置以及次数

```
var str = ’abcosidfnoiojisoo',
var index = str.indexOf('o');
var num = 0;
while(index !== -1) {
    console.log(index);
    num++;
    index = str.indexOf('red', index + 1);
}
```

**根据索引号返回字符**：

[Untitled](Untitled%20e45cf0780fbb4709a28a660d62b137bf.csv)

例子：统计出现最多的字符和次数

核心算法：利用 charAt() 遍历这个字符串

把每个字符都存储给对象，若没有该属性就为 1，若存在了就 +1

```
var str = 'abcoefoxyozz';
var obj = {};
for (var i = 0; i < str.length; i++) {
    var chars = str.charAt(i); //chars 是字符串的每一个字符
    if (obj[chars]) {
        obj[chars]++;  // 属性存在则加一
    } else {
        obj[chars] = 1;
    }
}

var max = 0;
var ch = '';
for (var k in obj) {
    if (obj[k] > max) { // k是属性名
        max = obj[k]; // obj[k] 是属性值
        ch = k;
    }
}
```

**字符串操作方法**：

[Untitled](Untitled%20df053e5d26a942c1b3bb6180a38d4a38.csv)

```
//把所有o都替换为i
var str = 'ooooooooo';
while (str.indexOf('o') != -1) {
    str.replace('o','i');
}
//分隔符举例
var str = 'green-red-pink-blue';
console.log(str.split('-')); //[green,red,pink,blue]
```

### **简单数据类型和赋值数据类型**

简单类型又叫做基本数据类型或者 **值类型**：在存储中就是值的本身

string, number, boolean, undefined, null

复杂类型又叫做 **引用类型**：在存储时变量中存储的仅仅是地址（引用）

通过 new 关键字创建的对象（系统对象、自定义对象），如 Object、Array、Date等

栈（操作系统）：由操作系统自动分配释放存放函数得参数值、局部变量得值等，**简单数据类型存放到栈里面**

堆（操作系统）：存储复杂类型（对象），一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收，**复杂数据类型存放到堆里面**

简单数据类型传参：函数的形参可以看作一个变量，当我们把一个值类型作为参数传给函数得形参时，其实是把变量在栈空间里得值**复制了一份给形参**，在方法内部对形参做任何修改都不会影响到外部变量

复杂数据类型传参：函数得形参也可以看作是一个变量，当我们把引用类型变量传给形参时，其实是把变量在栈空间里保存得地址复制给了形参，**实参和形参保留得是同一个堆地址**，所以操作的是同一个对象

```
function Person(name) {
    this.name = name;
}
function f1(x) {
    console.log(x.name); // 2. 刘德华
    x.name = '张学友';
    console.log(x.name); // 3. 张学友
}
var p = new Person('刘德华');
console.log(p.name); // 1. 刘德华
f1(p);
console.log(p.name); // 4.张学友
```