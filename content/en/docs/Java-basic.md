---
title: Java Basic
slug: Java-Basic
lastmod: 2025-07-01T00:00:00+00:00
---

面向对象的三大基本特性：封装、继承、多态

## 1. Java 编译和运行

<img src="/img/JavaBasic/1.png" width="700" style="border-radius: 5px; margin-top: 5px; margin-bottom: 0px;">

**编写**：在 VSCode 中编写好代码文件 hello.java  
**编译**：利用 JDK 中 javac.exe 执行 javac hello.java 命令，将代码文件 (hello.java) 编译为字节码文件 (hello.class)  
**加载**：利用 JDK 中 java.exe 执行 java hello 命令启动 JVM，JVM 使用类加载器，将字节码文件加载到内存中， JVM 初始化运行时环境，包括堆、栈、方法区等，准备执行 Java 程序  
**JIT生成机器码**：JVM 的解释器和即时编译器 (JIT Compiler) 来执行字节码。解释器逐行解释字节码，而 JIT 编译器则将热点代码编译成机器码以提高执行效率。JVM 内置的垃圾回收器（Garbage Collector）会自动管理内存，回收不再使用的对象  
**执行**：机器码在物理 CPU 上执行  


<img src="/img/JavaBasic/2.png" width="600" style="border-radius: 5px; margin-top: 20px; margin-bottom: 0px;">

## 2. Java 基础知识

### 2.1 基本数据类型
八种基本数据类型：

| 数据类型      | 大小（位）  | 默认值        | 表示范围或精度            | 示例值                 |
| --------- | ------ | ---------- | ------------------ | ------------------- |
| byte    | 8      | 0          | -128 ~ 127         | `byte b = 10;`      |
| short   | 16     | 0          | -32,768 ~ 32,767   | `short s = 100;`    |
| int     | 32     | 0          | -2³¹ ~ 2³¹-1       | `int i = 1000;`     |
| long    | 64     | 0L         | -2⁶³ ~ 2⁶³-1       | `long l = 10000L;`  |
| float   | 32     | 0.0f       | 约 6-7 位小数精度        | `float f = 3.14f;`  |
| double  | 64     | 0.0d       | 约 15 位小数精度         | `double d = 2.718;` |
| char    | 16     | '\u0000' | 单个 16 位 Unicode 字符 | `char c = 'A';`     |
| boolean | 1（逻辑位） | false      | true/false   | `boolean b = true;` |

### 2.2 数据转换

- 隐式转换：低精度的数据类型转换为高精度的数据，会自动转换，无需显式声明
- 强制转换：高精度的数据类型转换为低精度的数据，需要显式转换，否则编译错误

```java
int i = 100;
long l = i;      // int 自动转换为 long
float f = l;     // long 自动转换为 float

double d = 3.14;
int i = (int) d; // d 被强制转换为 int，结果是 3（小数被截断）
```

### 2.3 运算符
```java
+ - * / % && || ! != > >= < <=
```

### 2.4 选择结构

选择结构根据条件的真假决定执行哪部分代码

| 结构           | 语法形式                                                         | 说明                |
| ------------ | ------------------------------------------------------------ | ----------------- |
| `if`         | `if (condition) { statements; }`                             | 条件为真时执行语句块        |
| `if else`    | `if (condition) { statements1; } else { statements2; }`      | 条件为真执行语句1，否则执行语句2 |
| `else if` | `if (cond1) {...} else if (cond2) {...} else {...}`          | 多条件判断             |
| `switch`     | `switch (variable) { case value1: ... break; default: ... }` | 多分支选择，适用于枚举值或整数判断 |

举例：
```java
int score = 85;
if (score >= 90) {
    System.out.println("优秀");
} else if (score >= 60) {
    System.out.println("及格");
} else {
    System.out.println("不及格");
}
```

### 2.5 循环结构

循环结构用于重复执行一段代码，直到满足某个条件

| 结构         | 语法形式                                            | 说明                 |
| ---------- | ----------------------------------------------- | ------------------ |
| `for`      | `for (init; condition; update) { statements; }` | 已知循环次数             |
| `while`    | `while (condition) { statements; }`             | 先判断条件再执行           |
| `do-while` | `do { statements; } while (condition);`         | 先执行一次，再判断是否继续      |
| `break`    | `break;`                                        | 跳出当前循环             |
| `continue` | `continue;`                                     | 跳过当前循环中的剩余语句，进入下一轮 |

举例：
```java
for (int i = 1; i <= 5; i++) {
    System.out.println("第 " + i + " 次循环");
}
```

### 2.6 自定义方法

修饰词 + 返回值 + 函数名 (形参) { 函数体 }  

### 2.7 函数重载 Overload

Overload 函数重载：在同一个类中，函数名可以相同，但是其参数的个数、类型、顺序有所不同，不能通过返回值来区别重载函数，不能有两个名字相同，参数类型也相同，却返回不同类型值的方法。

```java
public class OverloadExample {
    // 重载方法1：两个 int 参数
    public static int add(int a, int b) {
        return a + b;
    }

    // 重载方法2：三个 int 参数
    public static int add(int a, int b, int c) {
        return a + b + c;
    }

    // 重载方法3：两个 double 参数
    public static double add(double a, double b) {
        return a + b;
    }

    public static void main(String[] args) {
        System.out.println(add(2, 3));          // 调用 int,int 版本 → 输出 5
        System.out.println(add(2, 3, 4));       // 调用 int,int,int 版本 → 输出 9
        System.out.println(add(2.5, 3.7));      // 调用 double,double 版本 → 输出 6.2
    }
}
```

## 3. Java 面向对象

对象 = 属性 + 方法  
变量定义的变迁：基本类型 -> 结构体 -> 类

### 3.1 类结构

类是java最基础的逻辑单位，用来定义对象的属性和行为，使用规则如下：  
- 一个类包括属性，方法，构造函数和析构函数
- Java 中所有的内容都是需要放在 class 的范围内，不允许游离在 class 以外
- 一个 java 文件里可以有多个 class，但是只能有一个 public class
- 一个 class 最多只能有一个 main 函数，是程序的入口，也可以没有 main 函数，没有 main 函数的类不能主动执行，但可以被动调用执行。其中 main函数不算成员函数，无法被其他方法和类调用

```java
public class Person {
    // 属性
    int age;
    String name;
    // 构造函数
    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }
    // 方法
    public void sayHello() {
        System.out.println("Hello, my name is " + name + ".");
    }
}
```

### 3.2 对象

类（Class）是对象的模板或蓝图，而对象（Object）是类的实例  
类定义了对象的属性和行为，对象则是用类创建出来的实际实体

```java

// 创建对象
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person(25, "Alice");  // 创建对象
        p1.sayHello();             // 调用方法
    }
}
```
对象初始化：

```java
Person p = new Person(); // 创建对象，调用无参构造函数
Person p = new Person("Alice", 20); // 使用构造方法初始化对象
```

### 3.3 引用类型

基本类型存储的是值本身，而引用类型存放的是对象的地址，Java 的对象就是引用类型  
当你把一个对象赋值给另一个变量时，两个变量会引用同一个对象，改变其中一个变量引用的对象内容

```java
Person a = new Person("Tom", 18);
Person b = a;  // b 引用了 a 指向的对象

b.name = "Jerry";
System.out.println(a.name);  // 输出 Jerry，a 和 b 引用同一个对象

```
判断引用类型是否相等：

| 判断方式           | 含义                                          | 示例代码          |
| -------------- | -------------------------------------------------- | ------------- |
| `==`        | 比较两个对象的引用地址是否相同，即是否指向同一个对象                | `a == b`      |
| `.equals()`  | 比较两个对象的内容是否相等。如果类没有重写 `equals` 方法，则行为等同于 `==`。 | `a.equals(b)` |

举一个例子：

```java
class Person {
    String name;
    @Override
    public boolean equals(Object obj) {
        if (obj instanceof Person) {
            Person other = (Person) obj;
            return this.name.equals(other.name);
        }
        return false;
    }
}

Person p1 = new Person("Tom");
Person p2 = new Person("Tom");

System.out.println(p1 == p2);        // false，因为是两个不同的对象
System.out.println(p1.equals(p2));   // true，重写了 equals，比较内容
```

### 3.4 构造函数

构造函数（Constructor）是一种特殊的类方法，用于创建对象并进行初始化操作

- 构造函数名称必须和类名一样，且没有返回值
- Java 一个类可以有多个不同参数的构造函数
- Java 有构造函数，没有析构函数，JVM 会自动回收所分配的变量的内存
- 每个子类的构造函数第一句话，都默认调用父类的无参构造函数 super()，除非子类的构造函数第一句话就是 super()

```java
class Person {
    String name;
    int age;
    // 构造函数1：无参
    Person() {
        name = "unknown";
        age = 0;
    }
    // 构造函数2：有参
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### 3.5 访问修饰符

在 Java 中，类的属性可以使用不同的访问修饰符（如 private、public、protected）来控制访问权限  
这些修饰符用于实现封装（encapsulation），保护数据不被非法访问

| 修饰符         | 同类中 | 同包中 | 子类中 | 跨包访问 |
| ----------- | --- | --- | --- | ---- |
| `private`   | √   | ×   | ×   | ×    |
| 默认（无）       | √   | √   | ×   | ×    |
| `protected` | √   | √   | √   | ×    |
| `public`    | √   | √   | √   | √    |

### 3.6 this 关键字

在 Java 中，this 是一个关键字，代表当前对象的引用。在类的内部使用，用来区分成员变量和传进来的参数等

**1. 区分成员变量和局部变量**  

当方法或构造函数的参数与成员变量重名时，使用 this 来明确表示成员变量
```java
public Person(String name) {
        this.name = name; // this.name 是成员变量，name 是构造函数参数
    }
```
**2. 在对象内部调用其他方法**  

调用当前对象的 sayHello 方法，或者构造函数之间相互调用，也可以省略 this
```java
public void greet() {
    this.sayHello(); 
}

public void sayHello() {
    System.out.println("Hello!");
}
```
**3. 返回当前对象** 

常用于链式调用
```java
public class Counter {
    private int count = 0;

    public Counter increment() {
        this.count++;
        return this; // 返回当前对象
    }

    public void print() {
        System.out.println("Count: " + count);
    }
}

// 使用示例
Counter c = new Counter();
c.increment().increment().print(); // Count: 2
```

注意：静态方法体中不能使用this关键字。非静态方法中可以用 this 关键字访问静态属性，静态方法体中不能使用 this 关键字访问静态属性，比如说 public static void main(String args[]) {}

## 4. Java 类的继承和接口

### 4.1 继承 extends 

Java 中类的继承是面向对象编程的核心特性之一  
它允许一个类（子类）继承另一个类（父类）的属性和方法，从而实现代码的复用、扩展和多态

**1. 继承的特点**

- 单根继承原则：一个类只能继承一个父类
- 支持多层继承：可以继承多层结构，如 class A → B → C
- 子类继承父类，父类的父类，所有的属性和方法，但不能直接访问private成员，但可以通过调用父类的方法来访问父类的私有的成员属性

**2. 基本语法**
```java
class Animal {
    public void eat() {
        System.out.println("Animal is eating");
    }
}
class Dog extends Animal {
    public void bark() {
        System.out.println("Dog is barking");
    }
}

Dog dog = new Dog();
dog.eat();  // 继承自 Animal
dog.bark(); // 自己定义的方法

```

**3. 使用 super 访问父类**
- super() 调用父类的构造函数，必须在子类构造函数的第一行
- super.方法名() 调用父类的方法。如果构造函数的第一句话不是super，编译器会自动增加一句super()，如果构造函数第一句是程序员自己写的super语句，编译器就不会自动增加了

```java
class Dog extends Animal {
    public Dog() {
        super("Dog"); // 调用父类构造函数
    }

    @Override
    public void sleep() {
        super.sleep(); // 调用父类方法
        System.out.println("Dog sleeps");
    }
}
```
### 4.2 重写 override

重写是指子类对父类继承的方法进行重新实现，它允许我们根据子类的需求，改变从父类继承来的方法行为

规则：
| 规则                                   | 说明                                        |
| ------------------------------------ | ----------------------------------------- |
| 方法名相同                                | 子类方法必须与父类被重写的方法名称相同                       |
| 参数列表相同                               | 参数类型、顺序、个数都要一致                            |
| 返回值类型相同                       | Java 5 起支持协变返回类型（covariant return type）   |
| 访问权限不能更严格                            | 可以更宽松（如从 protected 变成 public），不能变得更严格 |
| 不能重写 static、final 或 private 方法 | 这些方法不能被子类修改                               |
| 可以添加或保留 @Override 注解               | 编译器会检查是否真的在重写父类方法，避免错误                    |

举例：

```java
class Animal {
    public void makeSound() {
        System.out.println("Some sound");
    }
}
class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof");
    }
}
```

### 4.3 抽象类 abstract

**完整的类:** 所有定义的方法都实现了，只有完整的类才能被实例化，被 new 出来

**抽象类 (abstract class)**: 暂时还有方法没有实现，被定义为抽象类，类和抽象方法都需要用 abstract 关键字来修饰

**抽象类特点**: 抽象类不能实例化对象，除此之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。子类继承抽象类，如果不能完全实现父类的所有 abstract 方法，那么子类也必须被规定为抽象类

```java
public abstract class Shape {
    int area;

    // 抽象方法：子类必须实现
    public abstract void calArea();
    public abstract void draw();
    public abstract String getName();

    // 非抽象方法：子类可以继承或重写
    public void printArea() {
        System.out.println("Area: " + area);
    }
    public void setArea(int area) {
        this.area = area;
    }
}
```
### 4.4 接口类 interface

**接口类 (interface class)**: 一个类中所有抽象方法都没实现，那这个类就是接口类，用 interface 关键字来修饰  
**接口类的特点**: 
- 接口没有构造函数，类和方法必须是 public
- 不能有普通成员变量，但可以有 public static final 常量
- 一个类只能继承 extends 一个类，但是可以实现 implements 多个接口，class C implements A, B
- 一个接口可以继承多个接口，关键字用 extends，interface B extends A1, A2
- 类实现接口，就必须实现所有未实现的方法，否则是抽象类

定义接口：
```java
public interface Animal {
    void eat();       
    void sleep();     
    void move();      
    void makeSound(); 
    void reproduce(); 
}
```
实现接口：
```java
public class Dog implements Animal {
    @Override
    public void eat() {
        System.out.println("Dog eats bones");
    }

    @Override
    public void sleep() {
        System.out.println("Dog sleeps");
    }
}
```

### 4.5. 父子类型转换

子类和父类之间的转型（类型转换）是面向对象编程的重要机制，通常分为向上转型（Upcasting）和向下转型（Downcasting）  

1. **向上转型**：子类对象转换为父类类型，自动进行，不需要强制类型转换符

```java
// 正确情况 1
Animal obj1 = new Dog(); // 向上转型，自动进行

// 正确情况 2 
Dog dog = new Dog();
Animal animal = dog; 
animal.speak();   // 正确：可调用父类的方法
animal.bark();    // 错误：编译器无法识别子类特有的方法
```

2. **向下转型**：父类引用转换为子类类型，强制进行，必须加上类型转换符。如果父类引用不是实际指向的那个子类，会抛出 ClassCastException
```java
// 正确情况
Animal animal = new Dog(); // 实际是 Dog 对象
Dog dog = (Dog) animal;    // 向下转型，强制转换
dog.bark();                // 现在可以调用子类特有的方法

// 错误情况 1 
Animal animal = new Animal(); 
Dog dog = (Dog) animal; // 编译通过，运行时抛出 ClassCastException

// 错误情况 2
Dog obj2 = new Animal(); //illegal

```
### 4.6 多态
面向对象编程的核心特性：封装、继承、多态   
多态是对于同一个行为，不同的子类对象具有不同的表现形式。同一个接口，使用不同的实例而执行不同操作
- 提高代码复用性和可维护性，简化代码结构
- 运行时动态绑定，动态决策调用哪个方法
- 配合接口编程，降低耦合度

```java
class Shape {
    void draw() {}
}
class Circle extends Shape {
    void draw() {
        System.out.println("Circle.draw()");
    }
}
class Square extends Shape {
    void draw() {
        System.out.println("Square.draw()");
    }
}
class Triangle extends Shape {
    void draw() {
        System.out.println("Triangle.draw()");
    }
}
```

## 5. Java 常量管理

### 5.1 静态变量 static 

在 Java 中，static 是一个关键字，用来修饰类的变量、方法、内部类，表示这些成员属于类本身，而不是某个具体对象

**1. 静态变量**
- 静态变量属于类本身，所有对象共享一份内存
- 常用来记录类的全局状态，比如实例计数器、全局配置等
- 不需要创建对象就能访问：Person.count

```java
class Person {
    static int count = 0; // 静态变量
    public Person() {
        count++; // 每创建一个对象，count++
    }
}
```

**2. 静态方法**

- 静态方法也不依赖于对象，可以通过类名直接调用 MathUtils.add(1, 2)
- 在静态方法中，只能使用静态变量，不能使用非静态变量，因为非静态成员属于对象
- 在静态方法中，不能使用非静态方法，非静态方法可以直接引用静态方法

```java
public class StaticMethodTest {
    int a = 1;           // 非静态变量（属于对象）
    static int b = 2;    // 静态变量（属于类）
    public static void hello() {
        System.out.println(b);         // 正确，static 方法能访问 static 变量
        // System.out.println(a);      // 错误，static 方法不能访问非 static 变量
        // hi();                       // 错误，static 方法不能调用非 static 方法
    }
    public void hi() {
        hello();                    // 正确，可以调用 static 方法
        System.out.println(a);      // 正确，可以访问非 static 变量
        System.out.println(b);      // 正确，可以访问 static 变量
    }
    public static void main(String[] a) {
        StaticMethodTest.hello();  // 正确，静态方法通过类名调用
        // StaticMethodTest.hi();  // 错误，不能通过类名调用非静态方法
    }
}
```

**3. 静态代码块**

- 静态代码块在类加载时执行一次，可以用于初始化静态变量
- 无论创建多少个对象，静态代码块只执行一次
- 执行顺序：static块 > 匿名块 > 构造函数
```java
class StaticBlock {
    // 静态代码块
    static {
        System.out.println("static block");
    }
    // 匿名代码块
    {
        System.out.println("anonymous block");
    }
    // 构造函数
    public StaticBlock() {
        System.out.println("constructor function");
    }
}
// 最终输出
static block
anonymous block
constructor function
```

**4. 静态内部类**
- 静态内部类不依赖外部类的实例
- 可以直接通过 Outer.Inner 创建对象：new Outer.Inner()
```java
class Outer {
    static class Inner {
        void sayHi() {
            System.out.println("Hi from static inner class");
        }
    }
}
```

### 5.2 单例模式 Singleton

限定某一个类在整个程序运行过程中，只能保留一个实例对象在内存空间

采用 static 来共享对象实例

采用 private 构造函数，防止外界 new 操作

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714194216756.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714194216756.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714194247263.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714194247263.png)

双等号：指针相等

## **3. final**

final类：不能被继承

```
final public class Father{
}
class son extends Father{
}//Error
```

final方法：父类中如果有final的方法，子类中不能改写此方法

final变量：不能再次赋值

如果是基本型别的变量，不能修改其值

如果是对象实例，那么不能修改其指针(但是可以修改对象内 部的值

```
final int a = 5;
a = 10;// Error

public class FinalObj{
    int a = 10;
    public static void main(String[]){
        final FinalObj obj = new FinalObj();
        obj.a = 20;//OK
        obj = new FinalObj();//Error
    }
}
```

## **4. 常量设计和常量池**

Java没有constant关键字

Java中的常量：public static final

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714195801545.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714195801545.png)

一种特殊的常量：接口内定义的变量默认是常量

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714195844004.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714195844004.png)

常量池：相同的值只存储一份，节省内存，共享访问

基本类型的包装类 ：Boolean，Byte，Short，Integer，Long，Character，Float，Double

Boolean： true, false

Byte, Character : \u0000--\u007f (0—127)

Short, Int, Long：-128~127

Float，Double：没有缓存(常量池)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714201247081.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714201247081.png)

java为常量字符串都建立常量池缓存机制

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714201704194.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714201704194.png)

基本类型的包装类和字符串有两种创建方式，这两种创建方式导致创建的对象存放的位置不同

1. 常量式(字面量)赋值创建，放在栈内存 (将被常量化)
    
    ```
    Integer a = 10;
    String b = "abc";
    ```
    
2. new对象进行创建，放在堆内存 (不会常量化)
    
    ```
    Integer c = new Integer(10);
    String d = new String("abc");
    ```
    

举例1：

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202232334.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202232334.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202542879.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202542879.png)

举例2：

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202936693.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202936693.png)

## **5. 不可变类型**

不可变对象(Immutable Object) ：一旦创建，这个对象（状态/值）不能被更改了，其内在的成员变量的值就不能修改了

典型的不可变对象 ：

八个基本型别的包装类的对象 ，String，BigInteger和BigDecimal等的对象

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714203428527.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714203428527.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714203514101.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714203514101.png)

不可变对象，也是传指针(引用)

由于不可变，临时变量指向新内存，外部实参的指针不改动

## **6. String**

字符串内容比较：equals方法

是否指向同一个对象：指针比较==

StringBuffer/StringBuilder 的对象都是可变对象

StringBuffer(同步，线程安全，修改快速)

StringBuilder(不同步，线程不安全，修改更快)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714204222264.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714204222264.png)

# **第七章 package、import**

## **1. package**

Note:

1. 文件所在的目录必须要与其包名一致。否则虽然编译能通过但是运行不能通过
2. 运行class文件时前面需要加上所在包名，否则不能运行

## **2. 访问权限**

类的访问权限修饰符：只能是public和friendly(缺省)

属性：[public | protected | private] [static] [final]

方法：[public | protected | private] [static] [final | abstract］

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714205413103.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714205413103.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714205405545.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714205405545.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715034030171.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715034030171.png)

# **第八章 java常用类库**

## **1. 数字类**

java.lang.Math

Math类中的方法都是静态方法所以通过类名直接访问

```
public static int abs(int a) //Math.abs();
public static double ceil(double d)
public static double floor(double d)
public static int round(float f)
public static long round(double d) //Math.round(-10.5)
public static int max(int a, int b) //x = Math.max(1024, -5000);
public static int min(int a, int b)
public static double pow(double a, double b) //a的b次幂
public static double exp(double d) //求Math.E的d次幂
```

## **2. 字符串类**

## **3. 时间类**

## **4. 格式化类**

对话框：

```
import javax.swing.*;
public class InputTest2 {
    public static void main(String[] args) {
        String name = JOptionPane.showInputDialog("What is your name?");
        String input = JOptionPane.showInputDialog("How old are you?");
        int age = Integer.parseInt(input);//类型转换
        System.out.println("Hello," + name + ". Next year, you'll be " +(age + 1));
        System.exit(0);
    }
}
```

printf:

```
System.out.printf("%,.2f",10000.0 / 3.0); //按照浮点数格式输出，整数位用逗号分割，小数位为2位
System.out.printf("%tc",new Date());//%tc表示：t是日期输出的提示，c表示输出完整的日期
System.out.printf(“%1$s %2$tB %2$te, %2$tY”,“Due date:”,new Date());
%1$s表示：第一个参数即“Due date:”按照字符串来输出
%2$tB表示：第二个参数即“new Date()”输出英文的月
%2$te表示：第二个参数即“new Date()”输出两位数字日
%2$tY表示：第二个参数即“new Date()”输出四位数字年
```

java.text.Format:

日期：DateFormatter、SimpleDateFormat

数字：NumberFormat、DecimalFormat

字符串：MessageFormat

```
import java.text.Format.NumberFormat
NumberFormat N = NumberFormat.getInstance();
System.out.println(1000/3.0 + " " + 10000);
System.out.println(N.format(1000/3.0) + " " + N.format(10000));
输出为：
333.3333333333333 10000
333.333 10,000

NumberFormat C = NumberFormat.getCurrencyInstance();
System.out.println(C.format(1000));
C = NumberFormat.getCurrencyInstance(Locale.US);
System.out.println(C.format(1000));
输出为：
￥1,000.00
$1,000.00
```

```
import java.text.Format.DecimalForma
double avprice="28234.2534";
DecimalFormat df =new DecimalFormat("#.00");
String aveprice=df.format(avprice);
//整数保留不变，后面保留2位小数，不足则补0
```

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715070626732.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715070626732.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715065818464.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715065818464.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715065718523.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715065718523.png)

java.time.Format:

# **第九章 异常处理**

ArithmeticException: 除以零

ArrayIndexOutOfBoundException: 数组越界

FileNotFoundException: 打开不存在的文件

整数溢出、浮点数溢出、硬件错误、使用了不可用了IO设备等

```java
int[] br = new int[6];
try {
    System.out.println(br[10]);
}catch(Exception e) {
    System.out.print(e.getMessage());
}

//result：Index 5 out of bounds for length 6
```

异常可以理解为一个特殊的类

捕获并且处理异常的格式：

```java
try{
    ......
}catch(SomeExceptionType e){
    ......
}catch(Exception e){
    ......
}
```

如果try没有异常，catch直接跳过

如果异常第一个不匹配，就一直往下走

如果到最后还是没有匹配到错误类型就还是会报错

**finally**：

一定会执行的程序块

```java
try{
    ......
}
catch(){
    ......
}

finally{
    //无论发生什么异常，或者不发生异常，或者在try里直接return了，都会执行的部分
}
```

finally{}代码段在某些情况下是非常有用的，例如在异常发生之后我们还需要务必关闭数据库的连接，关闭文件，关闭已经打开的端口，关闭网络连接等

**Java常用的异常类：**

RuntimeException：

错误的转型（cast）：java.lang.ClassCastException

数组越界错误：java.lang.ArrayIndexOutOfBoundsException

空指针错误：java.lang.NullPointerException

数组元素类型错误：java.lang.ArrayStoreException

算术运算错误：java.lang.ArithmeticException

String转换成数字类型时的错误： java.lang.NumberFormatException

非RuntimeException:

文件读取越界：java.io.EOFException

文件没有找到：java.io.FileNotFoundException

URL链接错误：java.net.MalformedURLException

主机不可识别：java.net.UnknownHostException

**Exception类中的构造函数:**

```java
public Exception();
public Exception(String message);
```

**throw：**

一般与异常对象关联，我们可以在程序中需要的位置 自己抛出异常

如果程序执行中遇到了throw语句则正常的流程中断，转入到catch程序块中处理异常。

```java
NullPointerException ex = new NullPointerException()
throw ex;
```

如何得到异常描述信息：

在Exception的父类Throwable（java.lang包）中有定义

```java
String getMessag();
String toString();
Void printStackTrace();
```

```java
throw new Exception("Here's my Exception");

/* result 打印的内容是throw里面写的内容
e.getMessage(): Here's my Exception
e.toString(): java.lang.Exception: Here's my Exception
e.printStackTrace():java.lang.Exception: Here's my Exception at ExceptionMethods.main(ExceptionMethods.java:4)
*/
```

一般来说在一个方法的内部出现异常时，可以有两种处理方法：

1. 在方法的内部异常出现的地方，即throw语句出现的地方，用try语句捕获异常，catch语句处理异常。
2. 产生异常的方法不直接处理异常而是由调用该方法的其他方法来用try和catch程序块处理异常。
    
    ```java
    public class Test{
        public void division(){
            int num1 = 10;
            int num2 = 0;
            if(num2==0)
                throw new ArithmeticException();
            System.out.println(num1 / num2);
        }
        public static void main(String[] args) {
            Test t = new Test();
            try{
                t.division();
            }catch(ArithmeticException e){
                ......
            }
        }
    }
    ```
    

**使用自定义的异常：**

定义异常：

自定义的异常一般是Java系统中标准的Java Exception类或Throwable类的子类或者是你已经定义好的异常类的子类

```java
public class YourNewException extends Exception {}

class NotAValidAttribute extends Exception{
    public NoValidAttribute(){}
    public NoValidAttribute(String err){
        super(err);
    }
}
```

抛出异常：throws ,throw

1. 在方法名称后首先定义方法中将要抛出的异常类型列表
    
    throws语句位于方法头部的后面，用来声明方法内部已经抛出的并且还没有用try和catch程序块处理的异常的类型
    
2. 在需要报告异常的部分，创建相应的异常的实例，并且throw出该实例

```java
public void setName(String n) throws NotAValidAttribute {
    if (n == null)
        throw new NotAValidAttribute("employee's name is null");
    else
        name = n;
}
```

捕获异常：try，catch，finally

```java
try{
    ......
}
catch(MyExceptionType1 e){
    ......
}
catch(MyExceptionType2 e){
    ......
}
```

```java
class NotAValidAttribute extends Exception{
    public NotAValidAttribute (){}
    public NotAValidAttribute (String err){
    super(err);}
}

public class employee{
    private String name;
    private int age;

    public employee(){}
    public employee(String n, int a) throws NotAValidAttribute {
        this.setName(n);
        this.setAge(a);
    }
    public void setName(String n) throws NotAValidAttribute{
        name=n;
    }
    public void setAge(int a) throws NotAValidAttribute{
        if( a <= 18 || a >70)
            throw new NotAValidAttribute("error: employee's age must between 18 to 70");
        else age = a;
    }

    public static void main(String args[]){
        try{
            employee emp1 = new employee("Zhangcaiyi", 16);
        }catch (NotAValidAttribute e){
            System.err.println(e.getMessage());}
    }
}
```

该构造方法调用的setName，setAge等方法都抛出了自己的异常，而构造方法可以不在此时对这些异常处理，这种情况 下可以直接利用throws将异常抛出，留给后面的 调用该构造方法的main来处理异常（try-catch）

# **第十章 数据结构**

Array & ArrayList

存放相同类型的变量组合

定义方法：

```
int arrayname[];
int[] arrayname; //如果是局部变量不会自动初始化
public static int[] arrayname; //如果是属性，系统自动生成化为null

int[] arr = new int[4]; //定义并产生了由4个int组成的数组空间，初始化0，boolean类型为false
Car[] cars = new Car[6]; //定义并产生了由6个Car对象组成的数组空间，初始化null
```

初始化：

1. 使用循环语句
2. 统一初始化
    
    ```
    Car[] cars = {new Car(),new Car()};
    int[] arr = {1,2,3}
    ```
    
3. 动态统一初始化
    
    ```
    Car[] cars = new Car[]{new Car(),new Car()};
    ```
    

赋值：

java数组名也是引用，相同类型的数组名之间可以进行赋值操作

```
public class ArrayTest1 {
    public static int[] ar = new int[5];
    public static void main(String[] args) {
        int[] br = new int[6];
        br=ar;
        System.out.println(ar);
        System.out.println(br);
    }
}
//result，说明赋值之后内存空间是一样的
[I@2d363fb3
[I@2d363fb3
```

读取长度：arr.length

二分查找：看代码

对于基本类型、封装类、String类的数组可以调用java中array静态方法binarySearch直接完成查找

排序：看代码

复制：

1. 两个变量引用相同数组，指向相同的地址
    
    ```
    Car[] cars = new Car[5];
    for(int i=0,i<cars.length,i++)
        cars[i]=new Car();
    Car[] carsCopy = cars;
    ```
    
2. 复制到另外的数组，指向不同的地址
    
    ```
    System.arraycopy(fromArr,fromIndex,toArr,toIndex,count);
    System.arraycopy(cars,2,carCopy,0,3);
    //把cars从第2个下标开始，共3个元素，分别复制到carCopy空间从0-2处
    ```
    

数组可以作为用户自定义方法的参数

数组作为参数传入方法实际传入的是数组的引用，故Java中的方法可以改变数组中的元素的值。方法的返回值类型可以作为一个数组。 Java中返回的是一个数组的引用，指向一个array

```
public class ArrTest {
    private Car[] cars=new Car[] {new Car(), new Car()};
    private String[] arr ={"abc","def","ghi","lnn"};
    private int[] arrInt = {11,45,66,89};
    private void changeValue(String[] str, int i){
        System.out.println("before change：String[]:"+arr[i]);
        str[i] = "changed";
        System.out.println("After change：String[]:"+arr[i]);
    }
    private void changeValue(Car[] car_, int i){
        System.out.println("before change Car[]'sname:"+cars[i].carName);
        car_[i].carName ="red flag";
        System.out.println("After change Car[]'sname:"+cars[i].carName);
    }
    private void changeValue(int[] arrInt_,int i){
        System.out.println("before changeint[]:"+arrInt[i]);
        arrInt_[i] =100;
        System.out.println("after changeint[]:"+arrInt[i]);
    }

    public static void main(String[] args){
        ArrTest arrArg = new ArrTest();
        arrArg.changeValue(arrArg.arr,2);
        arrArg.changeValue(arrArg.cars,1);
        arrArg.changeValue(arrArg.arrInt,3);}
}
//result
before change：String[]:ghi
After change：String[]:changed
before change Car[]'sname:null
After change Car[]'sname:red flag
before changeint[]:89
after changeint[]:100
```

# **第十一章 文件读写**

## **1. 文件 java中的file类**

java的文件和目录都用file类，封装了对操作系统文件操作的功能

构造函数：

```java
File(String pathname)
File(String directoryPathname, String filename)
File(File directory, String fileName)
File(URI ur)
```

创建对象：

```java
File f=new File("D:\\mytest\\text.txt");
File f=new File("D:"+ File.separator +"mytest"+ File.separator +"test.txt");
```

抛出异常：

IOException

SecurityException

常用方法：

```java
import java.io.*

String getName()  返回文件名，不包括路径信息
String getPath()  返回文件的路径名
String getAbsolutePath()  返回绝对路径名。
long lastModified()  返回最后修改的时间
long length()  返回文件的长度

//文件或者目录的判断
boolean exists()       判断文件是否存在
boolean isFile()       判断是否为文件
boolean isDirectory()  判断是否为目录

//文件的读写判断
boolean canRead()   文件是否可读
boolean canWriter() 文件是否可写

//创建新的文件
boolean createNewFile() throws IOException 当文件不存在时，调用该方法创建新的文件
boolean mkdir()   创建一个由该文件对象指定的子目录
boolean mkdirs()  创建由该文件对象指定的目录

//文件属性的修改
boolean renameTo(File dest)：重命名
boolean setReadOnly():设置文件只读

//获取目录中的文件信息
String[] list(),如果file对象为一个目录，返回这个文件对象所包含的文件及子目录的名字。如果为一个文件则返回空(null)
File[] listFiles(),如果file对象为一个目录，返回这个文件对象所包含的文件及子目录构成的对象数组。如果为一个文件则返回空(null)
```

例子：

```java
//目录
File d = new File("E:\\temp");
if(!d.exists())
    d.mkdirs();
System.out.println(d.isDirectory());
//文件
File f = new File("E:\\temp\\test.txt");
if(!f.exists())
    try {
        f.createNewFile();
    } catch (IOException e) {
        e.printStackTrace();
    }
System.out.print(f.isFile());
//打印子列表
File[] fs = d.listFiles();
for(File i:fs)
    System.out.println(i.getPath());
```

## **2. 流 Stream**

java读写文件，只能以数据流的形式

File类和Stream类的区别：

File类主要用来描述系统中的文件在磁盘上的存储情况

Steam类主要是对文件的内容进行操作

## **3.java IO包**

节点类：直接操作文件类

InputStream：按照字节读取 FileInputStream子类

OutputStream：按照字节输出 FileoutputStream子类

Reader：按字符读取 FileRreader子类

Writer：按字符输出  FileWriter子类

转换类：字符到字节的转换

InputStreamReader 字节->字符

OutputStreamReader 字符->字节

装饰类：装饰节点类

DataInputStream, DataOutputStream

BufferInputStream, BufferOutputStream 缓存字节流

BufferReader, BufferWriter  缓存字符流

####

system类中的三类标准数据流：

```java
public static final InputStream in;//标准输入流
public static final PrintStream out;//标准输出流
public static final PrintStream err; //错误流
```

当在print方法的参数中传递的是一个对象时，系统将会调用该对象的toString()方法，然后将结果打印出来

输出重定向：

这意味着你程序运行的结果将会存放在result.txt中，此时在标准输出设备上将不会出现输出的结果

```java
System.err.println("路径:"+f.getPath());
System.err.println("大小:"+f.length()+" bytes" );
```

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714144629734.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714144629734.png)

## **4. 文本文件的读写**

**写文件：创建、写入数据、关闭**

用到三个类：

FileOutputStream  往文件写字节

OutputStreamWriter  字节和字符的转化

BufferedWriter 写缓冲区类，加速写操作 write() newline()

```java
FileOutputStream fos = null;
OutputStreamWriter osw = null;
BufferedWriter bw = null;
try {
    fos = new FileOutputStream("E:\\temp\\test.txt");
    osw = new OutputStreamWriter(fos,"UTF-8");
    bw = new BufferedWriter(osw);
    bw.write("我是");
    bw.newLine();
    bw.write("xxx");
    bw.newLine();
}catch(Exception e) {
    e.printStackTrace();
}finally {
    try {
        bw.close();
    }catch(Exception w) {
        w.printStackTrace();
    }
}
```

**读文件：打开，逐行读，关闭**

FileInputStream  往文件写字节

InputStreamReader  字节和字符的转化

BufferedReader 写缓冲区类 readLine()

```java
FileInputStream fis = null;
InputStreamReader isr = null;
BufferedReader br = null;
try {
    fis = new FileOutputStream("E:\\temp\\test.txt");
    isr = new OutputStreamWriter(fis,"UTF-8");
    br = new BufferedWriter(isr);
    String line;
    while((line=br.readLine())!=null){
        System.out.print(line);
    }
}catch(Exception e){
    e.printStackTrace();
}finally{
    try {
        br.close();
    }catch(Exception w) {
        w.printStackTrace();
    }
}
```

## **4. 二进制文件的读写**

写文件：

FileOutputStream

BufferedOutputStream

DataOutputStream：flush()，write()

```java
FileOutputStream fos = null;
Buffer
edOutputStream bos = null;
DataOutputStream dos = null;
try{
    fos = new FileOutputStream("E:\\temp\\test.txt");
    bos = new BufferedOutputStream(fos);
    dos = new DataOutputStream(bos);

    dos.writeUTF("a");
    dos.writeInt(20);
}catch(Exception e){
    e.printStackTrace();
}finally{
    try{
        dos.close();
    }catch(Exception e){
        e.printStackTrace();
    }
}
```

读文件：

FileInputStream

BufferedInputStream

DataInputStream：read()

## **5. 用文本流读取和写入文件**

读取Unicode信息的常用方法：BufferedReader

FileReader、FileWriter

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714181632838.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714181632838.png)

```java
class BufferedReaderDemo{
    public static void main(String args[]){
        try {
            FileReader fr = new FileReader("student.txt"); //源文件
            BufferedReader br = new BufferedReader(fr);
            while((read = br.readLine())!= null)
                System.out.println(read);
            fr.close();
            br.close();
        } catch (IOException ie){
            System.err.println(ie.getMessage());
        }
    }
}
```

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210924213859.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210924213859.png)

![https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210924215030.png](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210924215030.png)

```java
//BufferedWriter的方法
void close() Close the stream.
void flush() Flush the stream.
void newLine () Write a line separator. //换行
void write (char[] cbuf, int off, int len) Write a portion of an array of characters.
void write(int c) Write a single character.
void write (String s, int off, int len) Write a portion of a String.
```