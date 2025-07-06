---
title: C plus plus 
slug: C-plus-plus 
lastmod: 2025-07-01T00:00:00+00:00
---

1. ~~C++ 虚函数表~~
2. TCP/IP RTP RTCP
3. NV12/NV21 转换的 background
4. C++ 同或异或，数组里唯二的非成对数
5. Media codec 的工作流程

- 提纲
    
    ## **第 1 章：C++ 语言基础**
    
    - C++ 发展与 C 语言的区别
    - 编译环境搭建（GCC、Clang、MSVC）
    - 变量、常量、基本数据类型 (`int`, `double`, `char`, `bool`)
    - 类型转换（隐式与显式转换）
    - 运算符与表达式（算术、逻辑、位运算、`sizeof`、`decltype`）
    - 输入输出（`cin`, `cout`）
    
    ---
    
    ## **第 2 章：程序控制结构与函数**
    
    - 条件语句（`if-else`, `switch-case`）
    - 循环（`for`, `while`, `do-while`）
    - `break`, `continue`, `goto`
    - 函数的定义与调用
    - 作用域、存储类别（`static`、`extern`）
    - 递归与内联函数 (`inline`)
    - 函数指针
    
    ---
    
    ## **第 3 章：数组、指针与字符串**
    
    - 一维数组、多维数组
    - 指针基础（指针变量、指针与数组的关系）
    - 动态内存分配 (`new/delete`)
    - `std::string` 与 `cstring` 操作
    - `vector` vs. 传统数组
    - `decltype` 与 `auto`
    
    ---
    
    ## **第 4 章：面向对象编程（OOP）**
    
    - 结构体 (`struct`) 与类 (`class`) 的区别
    - 类与对象的基本概念
    - 构造函数、析构函数
    - 访问控制（`public`, `private`, `protected`）
    - `this` 指针与静态成员 (`static`)
    - 友元函数与友元类
    - 运算符重载（`+`, , `[]`, `()`, `<<`, `>>`）
    
    ---
    
    ## **第 5 章：继承、多态与虚函数**
    
    - 继承的基本概念（基类与派生类）
    - 构造函数与析构函数的执行顺序
    - `final` 与 `override` 关键字
    - 虚函数与多态（`virtual` 关键字）
    - 纯虚函数与抽象类
    - 虚函数表 (`vtable`) 与 `dynamic_cast`
    - `typeid` 和 `RTTI`（运行时类型识别）
    
    ---
    
    ## **第 6 章：标准模板库（STL）**
    
    - STL 容器（`vector`, `list`, `deque`, `map`, `set`）
    - 迭代器 (`iterator`) 的使用
    - 常见算法（`sort`, `find`, `count`）
    - `std::function` 与 `bind`
    - `Lambda` 表达式
    
    ---
    
    ## **第 7 章：内存管理与智能指针**
    
    - `new/delete` 与 `malloc/free` 的区别
    - `std::unique_ptr`（独占所有权）
    - `std::shared_ptr`（共享所有权）
    - `std::weak_ptr`（避免循环引用）
    - RAII（资源获取即初始化）
    
    ---
    
    ## **第 8 章：多线程编程**
    
    - `std::thread` 线程的创建与管理
    - 线程同步（`std::mutex`, `std::lock_guard`）
    - `std::condition_variable`（条件变量）
    - 死锁与 `std::unique_lock`
    - 线程池的实现
    
    ---
    
    ## **第 9 章：模板编程与高级特性**
    
    - 函数模板与类模板
    - 模板的特化与偏特化
    - 变长模板参数 (`template <typename... Args>`)
    - `constexpr`（编译期计算）
    - `concepts`（C++20 约束概念）
    
    ---
    
    ## **第 10 章：现代 C++ 特性与实战**
    
    - C++11：`auto`, `nullptr`, `lambda`, `move`
    - C++14：`generic lambda`, `return type deduction`
    - C++17：`if constexpr`, 结构化绑定
    - C++20：协程 (`coroutine`)、模块化 (`modules`)
    - `std::optional`, `std::variant`
    - 文件操作 (`fstream`, `ifstream`, `ofstream`)
    - C++ 项目实战（如简易 Web 服务器或线程池）

### 1. **语言基础**

- Hello World 基本结构
    
    ```cpp
    #include <iostream>
    using namespace std;
     
    // main() 是程序开始执行的地方
     
    int main()
    {
       cout << "Hello World"; // 输出 Hello World
       return 0;
    }
    ```
    
    - C++ 语言定义了一些头文件，这些头文件包含了程序中必需的或有用的信息。上面这段程序中，包含了头文件 **<iostream>**
    - 下一行 **using namespace std，**告诉编译器使用 std 命名空间。命名空间是 C++ 中一个相对新的概念
- C++ 发展与 C 语言的区别
    
    
    C++ 由 Bjarne Stroustrup 在 1979 年开发，最初是 C 语言的扩展，后来发展为独立的语言。它保留了 C 的高性能特点，同时增加了 **面向对象（OOP）、泛型编程（templates）、标准库（STL）、RAII 资源管理** 等特性
    
    | 特性 | C | C++ |
    | --- | --- | --- |
    | 编程范式 | 过程式编程 | 过程式 + 面向对象 + 泛型 |
    | 标准库 | stdio.h (printf) | iostream (cout) |
    | 内存管理 | malloc/free | new/delete + 智能指针 |
    | 结构体 | 仅数据，无成员函数 | struct 可包含函数 |
    | 封装 | 无访问控制 | public/private/protected |
    | 多态 | 无 | 虚函数 (virtual) |
- C++ 编译环境 GCC/Clang/MSVC
    
    常见的几种 C/C++ 编译器和工具链：GCC（GNU Compiler Collection）、Clang 和 MSVC（Microsoft Visual C++），但它们有很多不同之处，包括平台支持、编译性能、优化能力、错误诊断等方面。下面是详细对比
    
    | 编译器 | 平台 | 适用场景 |
    | --- | --- | --- |
    | GCC | 原生支持 Linux/Unix，可在 Windows(MinGW) 和 macOS 上使用 | Linux 服务器、嵌入式、开源项目
    传统 Unix 系统 |
    | Clang | 广泛兼容，支持 Linux、Windows、macOS，其中 Xcode 默认 Clang | macOS/iOS 开发（Xcode 默认用 Clang）
    LLVM 生态项目，性能分析 |
    | MSVC | Microsoft 开发，只用于 Windows | Windows 桌面应用、游戏（DirectX
    .NET 混合项目、Windows 内核开发 |
    
    | 目标 | GCC | Clang | MSVC |
    | --- | --- | --- | --- |
    | 编译 C++20 | `-std=c++20` | `-std=c++20` | `/std:c++20` |
    | 优化级别 | `-O2/-O3` | `-O2/-O3` | `/O2` |
    | 调试模式 | `-g` | `-g` | `/Zi` |
    | 架构优化 | `-march=native` | `-march=native` | `/arch:AVX2` |
    | 警告开关 | `-Wall -Wextra` | `-Wall -Wextra` | `/W4` |
    | 静态分析 | `-fanalyzer` | `clang-tidy` | `/analyze` |
    | 预处理 | `-E` | `-E` | `/P` |
- C++ 比 Java 高性能的原因
    
    C++ 的效率通常比 Java 高，尤其在需要高性能的场景（如实时通信和游戏开发），主要原因包括以下几个方面：
    
    ### 1. **更低的抽象层次**
    
    - **C++** 更接近底层硬件，它允许程序员直接操作内存和硬件资源（如指针、内存管理等），减少了额外的抽象层开销。
    - **Java** 是一种运行在 JVM（Java Virtual Machine）上的语言，这种额外的抽象层使得程序的执行速度稍逊一筹。
    
    ### 2. **手动内存管理**
    
    - **C++** 提供了完全的手动内存管理，允许开发者精准控制内存分配与释放。
        - 虽然更容易出错，但可以减少垃圾回收（Garbage Collection）的性能开销。
    - **Java** 使用自动垃圾回收器，这简化了内存管理，但在高性能场景下可能导致 **垃圾回收停顿（GC Pause）**，影响性能。
    
    ### 3. **零成本抽象**
    
    - **C++** 的设计哲学之一是“零成本抽象”，即编译器在生成机器代码时尽量消除多余的抽象层和性能开销。
    - **Java** 中的抽象（如类、接口、JVM 特性）可能会带来一些运行时的性能损耗。
    
    ### 4. **即时编译（JIT）与静态编译的差异**
    
    - **Java** 使用 **JIT 编译（Just-In-Time Compilation）**，在运行时将字节码编译为机器码，带来动态优化的可能性，但也增加了运行时的延迟。
    - **C++** 是静态编译语言，编译器在编译时生成高效的机器码，因此运行时性能更高。
    
    ### 5. **更高的硬件适配能力**
    
    - **C++** 程序直接编译为目标平台的机器码，可以利用硬件的全部能力(SIMD 指令集、多核优化等)
    - **Java** 依赖 JVM，不同平台的 JVM 实现可能性能差异，并且 JVM 对底层硬件的优化能力有限
    
    ### 6. **代码内联与优化**
    
    - **C++** 编译器可以在编译时对代码进行深度优化，例如内联函数、循环展开、消除死代码等。
    - **Java** 的动态优化虽然强大，但依赖于运行时环境，优化效果可能不如 C++ 编译器直接生成的高效代码。
    
    ### 7. **游戏和实时通信的特性需求**
    
    - 游戏和实时通信需要处理大量低延迟、高吞吐的数据处理任务。
    - **C++** 提供了更高的性能和灵活性，尤其在图形渲染、物理模拟、网络通信等方面。
    
    ### **总结**
    
    虽然 Java 在开发效率和跨平台能力上更出色，但在需要**极致性能**的场景（如实时通信、图形渲染、游戏引擎开发等），C++ 更能满足性能需求。因此，这些领域中通常选择 C++ 作为主要开发语言。
    
- 基本变量数据类型 int, float, double, char, bool, void, nullptr_t
    
    七种基本数据类型
    
    | **类别** | **类型** | **描述** | **大小** | **范围** |
    | --- | --- | --- | --- | --- |
    | **整数** | int | 标准整数 | 4 byte | -2,147,483,648 ~ 2,147,483,647 |
    |  | unsigned int | 无符号整数 | 4 byte | 0 ~ 4,294,967,295  |
    |  | short | 短整型 | 2 byte | -32,768 ~ 32,767 |
    |  | long | 长整型 | 4(32位平台)
    8(64位平台) | 2,147,483,648 
    9,223,372,036,854,775,807 |
    |  | long long | 更长整型 | 8 byte | -9,223,372,036,854,775,808 9,223,372,036,854,775,807 |
    | **浮点** | float | 单精度浮点数 | 4 byte | 通常约 7 位有效数字 |
    |  | double | 双精度浮点数 | 8 byte | 通常约 15-16 位有效数字 |
    |  | long double | 扩展精度浮点数 | 12/16 byte | 精度比 double 更高 |
    | **字符** | char | ASCII/UTF-8 | 1 byte | -128 ~ 127 |
    |  | unsigned char | 无符号字符 | 1 byte | 0 ~ 255 |
    |  | char8_t | UTF-8 字符 | 1 byte | UTF-8 编码（C++20） |
    |  | char16_t | UTF-16 字符 | 2 byte | UTF-16 编码（C++11） |
    |  | char32_t | UTF-32 字符 | 4 byte | UTF-32 编码（C++11） |
    |  | wchar_t | 宽字符 Unicode | 通常 2 或 4 字节 | 平台相关，用于存储宽字符 |
    | **布尔** | bool | 布尔值 | 1 byte | true 或 false |
    | **空** | void | 无类型/空 | N/A | 用于函数无返回值时 |
    | **指针** | nullptr_t | 空指针类型 | N/A | 指向无效地址（C++11 引入） |
    
    可以使用 **typedef** 为一个已有的类型取一个新的名字。下面是使用 typedef 定义一个新类型的语法
    
    ```cpp
    下面的语句会告诉编译器，feet 是 int 的另一个名称
    typedef int feet;
    
    现在，下面的声明是完全合法的，它创建了一个整型变量 distance
    feet distance;
    ```
    
- 变量类型限定符 const, static, restrict, mutable
    
    
    | 限定符 | 含义 |
    | --- | --- |
    | const | **const** 定义常量，表示该变量的值不能被修改。 |
    | volatile | 修饰符 **volatile** 告诉该变量的值可能会被程序以外的因素改变，如硬件或其他线程。。 |
    | restrict | 由 **restrict** 修饰的指针是唯一一种访问它所指向的对象的方式。只有 C99 增加了新的类型限定符 restrict。 |
    | mutable | 表示类中的成员变量可以在 const 成员函数中被修改。 |
    | static | 用于定义静态变量，表示该变量的作用域仅限于当前文件或当前函数内，不会被其他文件或函数访问。 |
    | register | 用于定义寄存器变量，表示该变量被频繁使用，可以存储在CPU的寄存器中，以提高程序的运行效率。 |
- 其他变量类型：枚举值 enum
    
    ```java
    #include <iostream>
    using namespace std;
    
    enum ErrorCode {
    	INITIALIZING_PREVIEW, //0
    	PREVIEW_INITIALIZATION_ERROR,
    	STARTING_PREVIEW,
    	PREVIEW_START_ERROR,
    	STOPPING_PREVIEW,
    	PREVIEW_STOP_ERROR,
    	PREVIEW_SET_ROTATION_ERROR
    };
    
    ErrorCode test(){
      return PREVIEW_STOP_ERROR;
    }
    int main()
    {
       cout << test(); //5
       return 0;
    }
    ```
    
- 变量的存储方式：堆(heap) vs 栈(stack)
    
    
    C++ 变量在内存中的存储方式主要由 **作用域** 和 **存储类型** 决定
    
    | 存储类别 | 关键字 | 作用域 | 生命周期 |
    | --- | --- | --- | --- |
    | 自动变量 | auto（默认） | 代码块内 | 进入块时创建，退出块时销毁 |
    | 静态变量 | static | 代码块/文件内 | 程序运行期间一直存在 |
    | 全局变量 | 无 | 文件内 | 程序运行期间一直存在 |
    | 动态分配变量 | new | 堆 | 手动管理，delete 释放 |
    
    **栈上 vs 堆上分配**
    
    - 栈（Stack）是一个内存区域，用于存储局部变量和函数调用的上下文。栈上的变量是自动分配的，它们的生命周期由函数的调用和返回控制。栈上的变量由编译器自动管理，作用域结束自动销毁。栈的大小有限，如果分配的栈空间过大，可能会发生栈溢出（stack overflow）
        
        ```cpp
        void myFunction() {
            int x = 10;  // x 存储在栈上
            double y = 3.14;  // y 存储在栈上
        }
        ```
        
    - 堆（Heap）是用于动态内存分配的区域，内存的分配和释放由程序员控制。堆上的变量是通过 动态内存分配 来创建的，通常使用 `new` 或 `malloc` 来分配内存，使用 `delete` 或 `free` 来释放内存。因此程序员需要小心避免内存泄漏（未释放的内存）或悬空指针（指向已释放内存的指针）
        
        ```cpp
        void myFunction() {
            int* p = new int;  // p 指向堆上的内存
            *p = 10;
            
            // 使用完后，必须手动释放内存
            delete p;  // 释放堆上的内存
        }
        ```
        
- 变量的类型转换：隐式 vs 显式
    
    
    | 特性 | 隐式转换（Implicit Conversion） | 显式转换（Explicit Conversion） |
    | --- | --- | --- |
    | 触发时机 | 编译器自动触发，无需程序员手动干预 | 由程序员手动插入转换代码 |
    | 转换方式 | 自动进行类型转换，不需要显式指定 | 程序员明确指定如何进行转换 |
    | 安全性 | 通常是安全的，但也可能导致数据丢失 | 可能导致未定义行为（如非法指针转换） |
    | 常见操作符 | 隐式转换不需要操作符 | 使用强制转换操作符如 type, static_cast, dynamic_cast, const_cast, reinterpret_cast |
    
    **隐式转换**
    
    由编译器自动进行的转换
    
    - 低精度的类型被自动转换为高精度：int → long, int → double
        
        ```cpp
        int a = 5;
        double b = a;  // 隐式转换，int 转换为 double
        ```
        
    - 将一个类型赋值给另一个兼容的类型：char → int, unsigned int → int
    
    **显式转换**
    
    通过程序员的强制指示来完成的类型转换，通常是使用 C 风格的强制转换（type）或 C++ 风格的转换操作符（如 static_cast, dynamic_cast, const_cast, reinterpret_cast）
    
    - C 风格的强制转换
        
        ```cpp
        double x = 3.14;
        int y = (int)x;  // C 风格强制转换，double 转换为 int
        cout << "y: " << y << endl;  // 输出: 3，丢失小数部分
        ```
        
    - C++ 风格的强制转换
        - **`static_cast`**：用于进行常规类型转换。是最常用的显式转换方式，适用转换兼容的类型
            
            ```cpp
            double x = 3.14;
            int y = static_cast<int>(x);  // C++ 风格强制转换
            ```
            
        - **`dynamic_cast`**：用于进行运行时的类型转换，通常与多态性（继承和虚函数）一起使用，用于转换指针或引用
            
            ```cpp
            Base* b = new Derived();
            Derived* d = dynamic_cast<Derived*>(b);  // 安全的向下转型
            ```
            
        - **`const_cast`**：用于去除或添加对象的 const 属性
            
            ```cpp
            const int x = 10;
            int* p = const_cast<int*>(&x);  // 去掉 const 属性
            ```
            
        - **`reinterpret_cast`**：用于将一个类型的指针转换为另一种类型的指针，甚至是完全不相关的类型。这是一种低级的转换，通常用于与硬件、内存操作等密切相关的应用
            
            ```cpp
            int* p = reinterpret_cast<int*>(0x1234);  // 将整数地址转换为指针
            ```
            
    
- 详解静态转换 static_cast
    
    static_cast 是 C++ 中四个命名强制类型转换操作符之一，它用于执行各种不同类型之间的转换
    
    1. 基础数据类型的转换：可以将一种基础数据类型转换为另一种基础数据类型。例如，将 double 转换为 int，或将 float 转换为 double
        
        ```cpp
        double d = 5.5;
        int i = static_cast<int>(d);  // i = 5
        ```
        
    2. **指向派生类**的指针或引用 → **指向基类**的指针或引用
        
        ```cpp
        class Base {};
        class Derived : public Base {};
        Derived derivedObj;
        Base* basePtr = static_cast<Base*>(&derivedObj);
        ```
        
    3. **指向基类**的指针或引用 → **指向派生类**的指针或引用：但这是不安全的，因为在转换过程中没有运行时检查。如果确实需要运行时检查，应使用 dynamic_cast
        
        ```cpp
        Base* basePtr = new Base();
        Derived* derivedPtr = static_cast<Derived*>(basePtr); // 不安全！
        ```
        
    4. 在有关联的类型之间进行转换：转换枚举值为整数
        
        ```cpp
        enum Color { RED, GREEN, BLUE };
        int value = static_cast<int>(GREEN);  // value = 1
        ```
        
- 详解类型重新解释转换 reinterpret_cast
    
    reinterpret_cast运算符是用来处理无关类型之间的转换，它会产生一个新的值，这个值会有与原始参数（expressoin）有完全相同的比特位。从上边对 reinterpret_cast 介绍，可以感觉出它是个很强大的运算符，因为它可以无视种族隔离，随便搞。但就像生物的准则，不符合自然规律的随意杂交只会得到不能长久生存的物种。随意在不同类型之间使用reinterpret_cast，也之后造成程序的破坏和不能使用
    
    [IBM的C++指南](http://publib.boulder.ibm.com/infocenter/compbgpl/v9v111/index.jsp?topic=/com.ibm.xlcpp9.bg.doc/language_ref/keyword_reinterpret_cast.htm) 里倒是明确告诉了我们 reinterpret_cast 可以用来作为转换运算符：
    
    - 从指针类型到一个足够大的整数类型
    - 从整数类型或者枚举类型到指针类型
    - 从一个指向函数的指针到另一个不同类型的指向函数的指针
    - 从一个指向对象的指针到另一个不同类型的指向对象的指针
    - 从一个指向类函数成员的指针到另一个指向不同类型的函数成员的指针
    - 从一个指向类数据成员的指针到另一个指向不同类型的数据成员的指针
    
    不过我在Xcode中测试了一下，事实上reinterpret_cast的使用并不局限在上边所说的几项的，任何类型的指针之间都可以互相转换，都不会得到编译错误
    
- 引用和指针的区别
- inline
    
    在C++中，**`inline`**是一个关键字，用于向编译器建议将函数内联展开。使用**`inline`**关键字修饰函数时，编译器会尝试在调用函数的地方直接展开函数的代码，而不是像普通函数一样生成函数调用。这样做的目的是为了提高程序的执行效率，减少函数调用的开销。
    
    通常情况下，编译器会根据函数的大小、复杂度和调用频率等因素来决定是否将函数内联展开，而使用**`inline`**关键字可以向编译器提供一种显式的提示，指示编译器尽可能地内联函数。
    
    在C++中，**`inline`**关键字可以在函数定义或者函数声明中使用，但它只是一种建议，编译器不一定会遵循。因此，即使使用了**`inline`**关键字，编译器也有可能选择不将函数内联展开。
    
    使用**`inline`**关键字的函数通常应该遵循一些限制条件，例如：
    
    1. 函数应该足够简单，以便展开时不会增加太多代码量。
    2. 函数应该频繁被调用，以提高内联的效益。
    3. 函数的定义必须在调用处可见，因为编译器需要展开函数的代码。
    
    一般来说，**`inline`**适用于较短小的函数或者在性能敏感的地方，但不应滥用，因为过多的内联可能会增加代码大小，并可能导致性能下降。
    
    "直接展开"指的是编译器在编译时将函数调用处直接替换为函数体的过程，而不是生成函数调用的指令。换句话说，就是将函数体的代码插入到每个调用处，而不是跳转到函数的入口点执行函数代码。
    
    举个例子，假设有一个简单的函数 **`square()`**：
    
    ```csharp
    inline int square(int x) {
        return x * x;
    }
    ```
    
    如果在程序中有一个函数调用 **`square(5)`**，而且编译器决定要直接展开该函数，那么编译器在编译时会将 **`square(5)`** 替换为 **`5 * 5`**。这样就避免了函数调用的开销，因为没有真正的函数调用过程，而是直接在调用处执行了函数体内的代码。
    
    直接展开可以提高程序的执行效率，特别是对于简单的、频繁调用的函数。因为没有了函数调用的开销，程序执行的速度会更快。但是，如果函数体过大或者被频繁调用的次数过多，直接展开可能会增加代码的大小，导致额外的内存开销，从而对程序的性能产生负面影响。因此，在使用**`inline`**关键字时，需要谨慎考虑函数的大小和调用频率，以便取得最佳的性能表现。
    

### 5. 标准模板库 STL

- What is STL
    
    C++ 标准模板库（Standard Template Library，STL）是一套功能强大的 C++ 模板类和函数的集合，它提供了一系列通用的、可复用的算法和数据结构
    
    - **代码复用**：STL 提供了大量的通用数据结构和算法，可以减少重复编写代码的工作
    - **性能优化**：STL 中的算法和数据结构都经过了优化，以提供最佳的性能
    - **泛型编程**：使用模板，STL 支持泛型编程，使得算法和数据结构可以适用于任何数据类型
    - **易于维护**：STL 的设计使得代码更加模块化，易于阅读和维护
    
- What’s in STL
    
    
    | **组件类型** | **定义** | **常见示例** | **应用场景** |
    | --- | --- | --- | --- |
    | 容器（Containers） | 存储和管理数据集合的类模板 | vector, map, set, deque, list, unordered_map | 数据存储、管理和访问 |
    | 算法（Algorithms） | 操作容器中元素的通用函数 | sort, find, for_each, accumulate  | 数据处理、计算和操作 |
    | 迭代器（Iterators） | 遍历容器元素的对象，连接容器与算法 | begin(), end(), ++, --, *  | 遍历、访问和操作容器元素 |
    | 函数对象（Function Objects） | 重载了 () 运算符的对象，可作为函数使用 | std::greater<>
    std::less<> | 自定义操作、比较器 |
    | 分配器（Allocators） | 管理内存分配和释放的对象 | std::allocator | 自定义内存管理策略 |
    | 适配器（Adapters） | 封装已有组件，改变其接口或行为 | stack, queue, priority_queue | 接口适配、行为修改
     |
    
    ### Container
    
    容器是用于存储和管理数据集合的类模板，提供了插入、删除、访问等操作
    
    - **顺序容器**（元素按插入顺序排列）
        - vector：动态数组，支持快速随机访问
        - deque：双端队列，支持两端快速插入/删除
        - list：双向链表，适合频繁的插入/删除操作
        - forward_list（C++11）：单向链表，内存开销更小
        - array（C++11）：固定大小的数组封装
        - string：用于处理文本字符串
    - **关联容器**（基于键值对，自动排序）
        - set：存储唯一元素，自动按键排序
        - map：存储键值对，键唯一，自动排序
        - multiset：允许重复元素的集合
        - multimap：允许键重复的映射
    - **无序关联容器**（基于哈希表，元素无序）：
        - unordered_set：存储唯一元素，使用哈希函数
        - unordered_map：存储键值对，键唯一，使用哈希函数
        - unordered_multiset：允许重复元素的无序集合
        - unordered_multimap：允许键重复的无序映射
    
    ### Algrithme
    
    STL 提供了一套通用算法，用于处理容器中的元素，如排序、查找、复制等
    
    - sort(begin, end)：对范围内的元素进行排序
    - find(begin, end, value)：查找等于指定值的元素
    - count(begin, end, value)：统计指定值的出现次数
    - for_each(begin, end, func)：对范围内的每个元素执行函数
    - copy(begin, end, dest)：将元素复制到另一个范围
    - remove(begin, end, value)：移除等于指定值的元素
    - accumulate(begin, end, init)（需包含 <numeric>）：计算范围内元素的总和
    
- std::map
    
    在C++中，std::map 是一个关联容器，它存储的元素是键值对，其中键是唯一的
    
    std::map内部使用红黑树实现，因此它的插入和查找操作的时间复杂度都是O(log n)
    
    1. **插入元素**：你可以使用 insert 函数或 [] 操作符或 emplace 插入元素
        
        如果容器中已经存在与新插入元素键相同的元素，函数不会替换已存在的
        
        ```java
        std::map<int, std::string> map;
        map.insert(std::make_pair(1, "one"));
        map[2] = "two";
        
        // 在容器中直接构造元素，比先创建元素然后插入容器更有效
        map.emplace(1, "one");
        map.emplace(2, "two");
        ```
        
    2. **查找元素**：你可以使用find函数查找元素。如果找到了元素，find会返回一个指向该元素的迭代器。如果没有找到元素，find 会返回 end()
        
        ```java
        auto it = map.find(1);
        if (it != map.end()) {
            std::cout << "Found: " << it->second << '\n';
        } else {
            std::cout << "Not found\n";
        }
        ```
        
    3. **遍历元素**：你可以使用范围 for 循环或迭代器遍历 std::map 的所有元素
        
        ```java
        for (const auto& pair : map) {
            std::cout << pair.first << ": " << pair.second << '\n';
        }
        ```
        
    4. **删除元素**：你可以使用 erase 函数删除元素
        
        ```java
        map.erase(1);
        ```
        
    5. **获取元素数量**：你可以使用 size 函数获取 std::map 的元素数量
        
        ```java
        std::cout << "Size: " << map.size() << '\n';
        ```
        
    6. **清空元素**：你可以使用 clear 函数清空 std::map 的所有元素
        
        ```java
        map.clear();
        ```
        
    
- std::string
    
    std::string 自动管理内存，不需要手动 new/delete
    
    创建
    
    ```cpp
    #include <iostream>
    #include <string>
    
    std::string s1 = "Hello";           // 直接赋值
    std::string s2("World");            // 构造函数初始化
    std::string s3 = s1 + " " + s2;     // 字符串拼接
    ```
    
    增删查改
    
    ```jsx
    str.length()
    str.empty()
    
    // 访问
    str[i]
    str.at(i)
    str.substr(pos, len)
    str.find("abc")
    
    // 添加
    str += "abc"
    str.append("abc")
    str.insert(pos, "inserted")
    
    // 替换
    str.replace(pos, len, "new")
    
    // 删除
    s.erase(pos, len)
    
    // 比较
    s1 == s2
    s1 < s2
    ```
    
    遍历和排序
    
    ```jsx
    std::string s = "hello";
    
    // 使用索引
    for (size_t i = 0; i < s.length(); ++i) {
        std::cout << s[i];
    }
    
    // 使用范围 for 循环
    for (char c : s) {
        std::cout << c;
    }
    ```
    
- std::string_view
    
    C++17 中我们可以使用 std::string_view 来获取一个字符串的视图，字符串视图并不真正的创建或者拷贝字符串，而只是拥有一个字符串的查看功能。std::string_view 比std::string 的性能要高很多，因为每个 std::string 都独自拥有一份字符串的拷贝，而std::string_view 只是记录了自己对应的字符串的指针和偏移位置。当我们在只是查看字符串的函数中可以直接使用 std::string_view 来代替 std::string
    
    ```cpp
    int main()
    {
     
        const char* cstr = "yangxunwu";
        std::string_view stringView1(cstr);
        std::string_view stringView2(cstr, 4);
        std::cout << "stringView1: " << stringView1 << std::endl; // yangxunwu
        std::cout << "stringView2: " << stringView2 << std::endl; // yang
    }
    ```
    
- std::vector
    
    std::vector 中的 capacity 和 size 都是用于描述容器的状态，分别表示不同的含义
    
    - size() 反映容器中已存储的实际元素数量。
    - capacity() 反映容器当前已分配的内存空间，可以容纳的最大元素数量。
    
    ### size()
    
    - **定义**：size() 返回当前 vector 中元素的数量，也就是容器内实际存储的元素个数。
    - **返回类型**：size() 返回一个 size_t 类型，表示容器中实际的元素数量。
    - **用途**：它告诉你当前容器中有多少个有效元素。
    
    ```cpp
    std::vector<int> vec = {1, 2, 3};
    std::cout << "Size: " << vec.size() << std::endl;  // 输出 Size: 3
    ```
    
    ### capacity()
    
    - **定义**：capacity() 返回当前 vector 能够容纳的元素数量，即容器在不重新分配内存的情况下可以存储的最大元素个数。
    - **返回类型**：capacity() 返回一个 size_t ，表示当前分配的内存可以存储多少个元素
    - **用途**：它反映了 vector 当前已分配的内存容量，不一定等于容器中元素的数量。
    
    ```cpp
    std::vector<int> vec = {1, 2, 3};
    std::cout << "Capacity: " << vec.capacity() << std::endl;  // 输出 Capacity: 3 或更大（可能会比 size 大）
    ```
    
    ### 动态扩容机制
    
    - 当你使用 push_back() 向 vector 中添加元素时，如果 size() 达到 capacity()，vector 会自动分配更多的内存空间（通常是扩展为原来的两倍）来容纳更多的元素。
    - 这意味着 capacity() 可能大于 size()，但 capacity() 不会小于 size()，它表示了容器当前能容纳的最大元素数。
    
    ### 举个例子：
    
    ```cpp
    cpp
    CopyEdit
    std::vector<int> vec;
    std::cout << "Initial size: " << vec.size() << ", capacity: " << vec.capacity() << std::endl;  // size: 0, capacity: 0
    
    vec.push_back(1);
    std::cout << "After push_back(1) -> size: " << vec.size() << ", capacity: " << vec.capacity() << std::endl;  // size: 1, capacity: 1
    
    vec.push_back(2);
    std::cout << "After push_back(2) -> size: " << vec.size() << ", capacity: " << vec.capacity() << std::endl;  // size: 2, capacity: 2
    
    vec.push_back(3);
    std::cout << "After push_back(3) -> size: " << vec.size() << ", capacity: " << vec.capacity() << std::endl;  // size: 3, capacity: 4 (可能会增加到 4)
    
    ```
    
    在这个例子中，`size()` 会随着 `push_back()` 的调用而增加，而 `capacity()` 可能会在某些情况下自动增加（当容器需要更多空间时）。
    
- std::list
- HRESULT
    
    定义：用于描述错误或警告的 32 位值
    
    常见的 HRESULT 值
    
    | 名称 | 说明 | 值 |
    | --- | --- | --- |
    | S_OK | 操作成功 | 0x00000000 |
    | E_FAIL | 未知故障 | 0x80004005 |
    | E_UNEXPECTED | 意外失败 | 0x8000FFFF |
    | E_ABORT | 操作已中止 | 0x80004004 |
    | E_ACCESSDENIED | 一般性的“访问被拒”错误 | 0x80070005 |
    | E_HANDLE | 无效的句柄 | 0x80070006 |
    | E_INVALIDARG | 一个或多个参数无效 | 0x80070057 |
    | E_NOINTERFACE | 不支持此类接口 | 0x80004002 |
    | E_NOTIMPL | 未实现 | 0x80004001 |
    | E_OUTOFMEMORY | 无法分配必要的内存 | 0x8007000E |
    | E_POINTER | 无效的指针 | 0x80004003 |

### Class & Object

- 类的分类：普通 / 抽象 / 接口 / 基类 / 派生 / 模版 / 静态
    
    在C++中，类是一种用户定义的数据类型，它具有数据成员（变量）和成员函数（方法）
    
    类是面向对象编程的基础，它支持封装、继承和多态
    
    - **普通类**
        
        ```cpp
        class MyClass {
        public:
            MyClass();   // 构造函数
            ~MyClass();  // 析构函数，释放资源
            int myVariable;      // 数据成员
            void myFunction() {  // 成员函数
                // 函数体
            }
        };
        ```
        
    - **抽象类（Abstract Class）**
        
        包含至少一个纯虚函数的类，不能实例化。作为其他类的基类，提供一个公共接口，供派生类实现
        
        任何继承 AbstractClass 的类都必须实现 pureVirtualFunction
        
        ```cpp
        class AbstractClass {
        public:
        		int myVariable; 
            virtual void pureVirtualFunction() = 0;  // 纯虚函数
        };
        ```
        
    - **接口类（Interface Class）**
        
        并没有明确的“接口”关键字，但接口类是指所有成员函数都是纯虚函数的类
        
        用于定义一组公共行为，不涉及具体实现。通过继承该接口类来实现这些行为
        
        与抽象类的区别：所有成员函数都是纯虚函数，不应该有任何成员变量，不包含任何实现，目的是为了实现统一协议、约定、行为要求
        
        ```cpp
        class Interface {
        public:
            virtual void method1() = 0;
            virtual void method2() = 0;
            virtual ~Interface() {}  // 虚析构函数
        };
        ```
        
    - **基类（Base Class）/ 派生类（Derived Class）**
        
        派生类是从基类继承而来的类。它继承了基类的成员并可以扩展或修改它们
        
        在 C++ 中，一个类可以同时继承多个类的成员
        
        ```cpp
        class ClassA {
        public:
            void functionA() {
                std::cout << "Function A" << std::endl;
            }
        };
        
        class ClassB {
        public:
            void functionB() {
                std::cout << "Function B" << std::endl;
            }
        };
        
        class Derived : public ClassA, public ClassB {
        public:
            void functionC() {
                std::cout << "Function C" << std::endl;
            }
        };
        ```
        
    - **模板类（Template Class）**
        
        支持泛型编程的类，允许在类定义时使用占位符类型，实际类型由用户在实例化时指定。MyClass 是一个模板类，可以用任何类型来实例化，类似于 MyClass<int>、MyClass<double> 等
        
        ```cpp
        template <typename T>
        class MyClass {
        private:
            T data;
        public:
            MyClass(T val) : data(val) {}
            T getData() {
                return data;
            }
        };
        ```
        
    - **静态类（Static Class）**
        
        将所有成员声明为静态的类，它无法实例化对象，通常用于封装一组相关的函数和常量
        
        ```cpp
        class StaticClass {
        public:
            static int count;
        
            static void increment() {
                count++;
            }
        };
        
        int StaticClass::count = 0;
        ```
        
- 对C++面向对象的理解：封装、继承、多态
    
    C++ 中的面向对象编程（OOP）主要包括三大特性：**封装、继承、多态**
    
- C++ malloc 和 new 的区别
    
    malloc/free 只分配内存，不调用构造/析构函数
    
    new/delete 既分配内存，又调用构造/析构函数
    
    - **malloc** 在 C/C++ 中只分配一块内存，从堆上开辟一块 raw memory，不会调用构造函数。需要手动用 free() 释放，也不会调用析构函数。返回的是 void*，你必须强转类型
        
        ```cpp
        Void* raw = malloc(sizeof(MyClass)); // 仅分配内存，不调用构造函数
        MyClass* obj = new (raw) MyClass()  // 手动调用构造函数
        
        obj -> ~MyClass()  // 手动调用析构函数
        free(obj);   // 释放内存
        ```
        
        对于数组的分配，malloc 只是开了一段连续内存，无法管理每元素，**不知道数组长度或元素类型**
        
        ```cpp
        int* arr = (int*)malloc(sizeof(int) * 5);
        ```
        
    - **new** 是在 C++ 中分配内存，加上调用对象的构造函数。删除时用 delete，自动调用析构函数。自动知道对象类型，不需要强制类型转换
        
        ```cpp
        MyClass* obj = new MyClass(); // 构造函数被正确调用
        delete obj;  // 析构函数也被调用，资源释放正确
        ```
        
        对于数组的分配，new[] 会调用每个元素的构造函数，delete[] 会调用每个元素的构造函数。
        
        注意始终用 new[] 配合 delete[]，不要用 new[] 配合 delete，这样会只析构一个对象
        
        ```cpp
        MyClass* arr = new MyClass[5]; // 会依次调用构造函数 5 次
        delete[] arr; // 会依次调用析构函数 5 次，正确释放资源
        ```
        
- C++ 多态的概念
    
    **多态（Polymorphism）** 是指通过统一的接口调用不同类型对象的行为。是面向对象中的核心特性。优点是接口统一，便于扩展和维护。实现“开闭原则”：代码对扩展开放，对修改封闭，提高代码复用性
    
    - **编译时多态**：通过函数重载、模板、运算符重载实现，在编译阶段就决定具体调用哪个函数
        
        ```cpp
        void print(int x) { std::cout << "int\n"; }
        void print(double x) { std::cout << "double\n"; }
        
        print(10);    // 调用 print(int)
        print(3.14);  // 调用 print(double)
        ```
        
    - **运行时多态**：通过继承 + 虚函数实现，通过基类指针或引用，去调用函数，在运行时决定调用哪个派生类的实现。底层原理是：编译器为含有虚函数的类生成虚函数表，每个对象有一个指针指向它所属类的虚函数表，通过虚函数表实现运行时的函数选择
        
        ```cpp
        #include <iostream>
        
        class Animal {
        public:
            virtual void speak() {
                std::cout << "Animal speaks\n";
            }
        };
        
        class Dog : public Animal {
        public:
            void speak() override {
                std::cout << "Dog barks\n";
            }
        };
        
        // 通过基类指针调用
        void makeItSpeakByPointer(Animal* a) {
            a->speak();  // 实际调用的是对象类型的 speak()
        }
        
        // 通过基类引用调用
        void makeItSpeakByReference(Animal& a) {
            a.speak();  // 同样调用的是对象类型的 speak()
        }
        
        int main() {
            Dog d;
        
            // 基类指针调用（运行时多态）
            makeItSpeakByPointer(&d);     // 输出：Dog barks
        
            // 基类引用调用（运行时多态）
            makeItSpeakByReference(d);    // 输出：Dog barks
        
            return 0;
        }
        ```
        
- 虚函数表
    
    虚函数表（VTable，Virtual Table）是 C++ 中实现运行时多态的一个机制。它是一个由指向虚函数的指针组成的表，用于支持通过基类指针或引用调用派生类的重写函数
    
    - 当类中包含虚函数 virtual ，编译器会为该类生成一个虚函数表 vtable
    - 每个实例化对象中有一个指向虚函数表 vtable 的指针，称为 vptr
- 访问修饰符 public、private、protected
    
    数据封装是面向对象编程的一个重要特点，它防止函数直接访问类的内部成员。类成员的访问限制是通过在类主体内部对各个区域标记 public、private、protected 来指定的
    
    ```python
    class Base {
     
       public:
     
      // 公有成员
     
       protected:
     
      // 受保护成员
     
       private:
     
      // 私有成员
     
    };
    ```
    
    - public 成员可以在类的外部访问
    - private(default) 成员只能在类的内部访问，只有类和友元函数可以访问私有成员
    - protected 成员可以在类及其派生类(子类)中访问
    
    一个 private 例子看看：
    
    ```python
    #include <iostream>
     
    using namespace std;
     
    class Box
    {
       public:
          double length;
          void setWidth( double wid );
          double getWidth( void );
     
       private:
          double width;
    };
     
    // 成员函数定义
    double Box::getWidth(void)
    {
        return width ;
    }
     
    void Box::setWidth( double wid )
    {
        width = wid;
    }
     
    // 程序的主函数
    int main( )
    {
       Box box;
     
       // 不使用成员函数设置长度
       box.length = 10.0; // OK: 因为 length 是公有的
       cout << "Length of box : " << box.length <<endl;
     
       // 不使用成员函数设置宽度
       // box.width = 10.0; // Error: 因为 width 是私有的
       box.setWidth(10.0);  // 使用成员函数设置宽度
       cout << "Width of box : " << box.getWidth() <<endl;
     
       return 0;
    }
    ```
    
    一个 protect 的例子
    
    ```python
    #include <iostream>
    using namespace std;
     
    class Box
    {
       protected:
          double width;
    };
     
    class SmallBox:Box // SmallBox 是派生类
    {
       public:
          void setSmallWidth( double wid );
          double getSmallWidth( void );
    };
     
    // 子类的成员函数
    double SmallBox::getSmallWidth(void)
    {
        return width ;
    }
     
    void SmallBox::setSmallWidth( double wid )
    {
        width = wid;
    }
     
    // 程序的主函数
    int main( )
    {
       SmallBox box;
     
       // 使用成员函数设置宽度
       box.setSmallWidth(5.0);
       cout << "Width of box : "<< box.getSmallWidth() << endl;
     
       return 0;
    }
    ```
    
- 非虚函数 override
    
    在 C++ 中，如果在子类中重写了一个与父类的非虚函数，将会发生以下情况：
    
    1. **遮蔽（隐藏）父类的同名函数**：
        - 子类中的同名函数会隐藏父类中的同名函数。这意味着在使用子类对象调用这个函数时，将会调用子类的实现，而不是父类的实现。即使你使用了子类对象来调用这个函数，父类的同名函数也不会被调用。
    2. **不具有多态性**：
        - 非虚函数不支持运行时多态性（即动态绑定），只有虚函数才能实现多态性。由于重写的函数不是虚函数，因此无论你如何调用它（通过基类指针或引用），都会直接调用它们各自所属类的版本，而不会有动态绑定的行为。
    3. **override 关键字的作用**：
        - override 关键字用于确保子类中的函数确实是在重写父类中的虚函数。它提供了一种编译时检查机制，避免了由于函数签名不匹配而导致的错误。在非虚函数中使用 override 关键字会导致编译错误
    
    ```sql
    #include <iostream>
    
    class Base {
    public:
        void foo() {
            std::cout << "Base::foo()" << std::endl;
        }
    };
    
    class Derived : public Base {
    public:
        void foo() {
            std::cout << "Derived::foo()" << std::endl;
        }
    };
    
    int main() {
        Base b;
        Derived d;
    
        b.foo();  // 调用 Base::foo()
        d.foo();  // 调用 Derived::foo()
    
        Base* bp = &d;
        bp->foo();  // 调用 Base::foo()，因为 Base::foo() 不是虚函数
    
        return 0;
    }
    
    ```
    
    在这个示例中：
    
    - `b.foo()` 调用 `Base::foo()`。
    - `d.foo()` 调用 `Derived::foo()`。
    - 当通过基类指针 `bp` 调用 `foo()` 时，即使 `bp` 实际上指向的是 `Derived` 对象，调用的仍然是 `Base::foo()`，因为 `foo()` 不是虚函数，不会进行动态绑定。
    
    因此，如果你希望函数具有多态行为，应将其声明为虚函数（`virtual`），并在子类中使用 `override` 关键字，以确保正确的重写行为。
    

### Advance structure

- 指针 Pointer
    
    指针是一个变量，其值为另一个变量的地址，即，内存位置的直接地址。就像其他变量或常量一样，您必须在使用指针存储其他变量地址之前，对其进行声明。
    
    1. **声明指针**：你可以声明一个指针，这里 p 是一个整型指针，它的值应该是一个地址，指向内存中的一个整数。所有指针的值的实际数据类型，不管是整型、浮点型、字符型，还是其他的数据类型，都是一样的，都是一个代表内存地址的长的十六进制数。
        
        ```python
        int    *ip;    /* 一个整型的指针 */
        double *dp;    /* 一个 double 型的指针 */
        float  *fp;    /* 一个浮点型的指针 */
        char   *ch;    /* 一个字符型的指针 */
        ```
        
    2. **初始化指针**：你可以在声明指针的时候给它一个地址，这里 x 是一个已经声明的整数，&x 是 x 的地址，所以 p 现在指向 x
        
        ```python
        int* p = &x;
        ```
        
    3. **解引用指针**：如果你有一个指针，并想要获取它指向的值，你可以使用 * 运算符，这里*p 是 p 指向的值，所以 y 现在和 x 有相同的值
        
        ```python
        int y = *p;
        ```
        
    4. **改变指针指向的值**：你可以通过解引用来改变指针指向的值，这会把 p 指向的值改为 10，所以 x 现在是 10
        
        ```python
        *p = 10;
        ```
        
    5. **指针的指针**：你可以有指向指针的指针，这里，pp 是一个指针的指针，它指向 p，
    所以 *pp 是 p，**pp 是 p 指向的值，即 x
        
        ```python
        int** pp = &p;
        ```
        
    6. **空指针**：一个指针可以是空的，它不指向任何东西，可以用 NULL 或 nullptr 来表示
        
        ```python
        int* p = nullptr;
        ```
        
    7. **动态内存分配**：在C++中，你可以使用 new 和 delete 来动态分配和释放内存。例如，下面第一条，分配了一个整数的空间，并把地址赋给 p
    然后，你可以使用 delete p 来释放这个空间
        
        ```python
        int* p = new int;
        delete p;
        ```
        
    8. **在函数中传递指针**
        
        ```python
        #include <iostream>
        #include <ctime>
         
        using namespace std;
         
        // 在写函数时应习惯性的先声明函数，然后在定义函数
        void getSeconds(unsigned long *par);
         
        int main ()
        {
           unsigned long sec;
         
         
           getSeconds( &sec );
         
           // 输出实际值
           cout << "Number of seconds :" << sec << endl;
         
           return 0;
        }
         
        void getSeconds(unsigned long *par)
        {
           // 获取当前的秒数
           *par = time( NULL );
           return;
        }
        ```
        
    
    注意：使用指针时要特别小心，因为错误的使用可能会导致程序崩溃或者其他未定义的行为，例如，解引用一个空指针或者没有初始化的指针
    
- C++ 智能指针
    
    智能指针是对裸指针的封装，自动管理内存生命周期，防止内存泄漏
    
    是 RAII（资源获取即初始化）思想的体现
    
    | **智能指针** | **特点说明** | 场景 |
    | --- | --- | --- |
    | std::unique_ptr<T> | 独占所有权，不能拷贝，只能转移。对象析构时自动释放资源。适合局部资源管理 | 更安全的管理局部资源 |
    | std::shared_ptr<T> | 多个指针共享同一对象，引用计数管理资源。最后一个引用释放时才销毁资源 | 多个模块/线程共享资源，如观察者模型 |
    | std::weak_ptr<T> | 弱引用，不增加引用计数，配合 shared_ptr 使用，避免循环引用 | 避免 shared_ptr 引用环 |
    - **unique_ptr**
        
        ```cpp
        #include <memory>
        #include <iostream>
        
        struct MyObject {
            MyObject()
            ~MyObject()
        };
        
        void basic_unique_ptr() {
        		std::unique_ptr<int> p = std::make_unique<int>(42);
        		*p = 100;
        } // 当 p 离开作用域(函数结束)，它会自动调用 delete
        
        void object_unique_ptr() {
            std::unique_ptr<MyObject> ptr1 = std::make_unique<MyObject>();
        
            std::unique_ptr<MyObject> ptr2 = ptr1; // ❌ 编译错误：不允许拷贝
            std::unique_ptr<MyObject> ptr2 = std::move(ptr1); // ✅ 所有权转移
        }
        ```
        
    - **shared_ptr**
        
        当多个函数、模块、线程需要共同使用并管理同一个对象时，就需要多个指针指向同一个对象
        
        比如观察者模式，事件发布/订阅，多个观察者都能使用同一个被观察者，两个线程都能使用同一个对象，并且对象会在最后一个线程用完后自动释放。
        
        又比如多线程池或回调中引用同一个对象，两个线程都能使用同一个对象，并且对象会在最后一个线程用完后自动释放
        
        ```cpp
        void basic_unique_ptr() {
        		std::shared_ptr<int> sp = std::make_shared<int>(42);
        		int count = sp.use_count();  // 引用计数
        		sp.reset();                  // 释放持有权
        }
        
        void object_shared_ptr() {
            std::shared_ptr<MyObject> p1 = std::make_shared<MyObject>();
            {
                std::shared_ptr<MyObject> p2 = p1;  // 引用计数 +1
            } // p2 析构，引用计数 -1
        } // p1 析构，对象销毁
        ```
        
        ```cpp
        std::shared_ptr<Data> data = std::make_shared<Data>();
        
        std::thread t1([data]() {
            data->process();
        });
        
        std::thread t2([data]() {
            data->save();
        });
        ```
        
    - **weak_ptr**
        
        为了避免 shared_ptr 引起的循环引用（memory leak），比如在观察者模式中，Subject 引用 Observer，Observer 引用 Subject。引用计数永远不为 0 → 对象永远不释放 → 内存泄漏
        
        ```cpp
        class Observer {
        public:
            Observer(std::shared_ptr<Subject> s) : subject(s) {}
        private:
            std::weak_ptr<Subject> subject; // ✅ 打破环
        };
        ```
        
    
- C++ 智能锁
    
    指 C++ 标准库提供的 RAII 风格锁管理器，用于自动加锁和释放锁，避免死锁或忘记释放锁
    
    | **锁类型** | **描述** |
    | --- | --- |
    | std::lock_guard<std::mutex>	 | 最简单的 RAII 锁，构造时加锁，析构时自动解锁 |
    | std::unique_lock<std::mutex> | 功能更强，支持延迟加锁、尝试加锁、手动释放等操作 |
    | std::scoped_lock (C++17) | 支持同时锁多个 mutex（防止死锁）	 |
    | 
    用于 `std::shared_mutex`，支持**读写锁**。多个线程可同时共享读锁，但写锁是互斥的
    
     |  |
    
    ```jsx
    #include <mutex>
    std::mutex m;
    
    void thread_safe_function() {
        std::lock_guard<std::mutex> lock(m);  // 构造时加锁，离开作用域自动解锁
        // 线程安全操作
    }
    
    void flexible_lock() {
        std::unique_lock<std::mutex> lock(m);  // 可 lock/unlock 手动控制
        lock.unlock(); // 手动释放
    }
    ```
    
- C++容器不是线程安全的，怎么解决？
- 读写锁和互斥锁
    1. 读写锁读的时候会加锁吗？
    2. 实现读写锁的时候会做二次加锁检测，你知道吗？看过源码吗？
- 二进制补码

### Thread

- 线程间通讯的方式
- 进程的虚拟地址空间划分
- 内存分段和分页
    
    内存分段（Segmentation）和分页（Paging）是操作系统常用的两种内存管理机制，用于将程序的逻辑地址映射到物理内存地址，解决内存空间利用率、进程隔离和内存保护等问题
    
- 线程安全和线程不安全
- 线程切换，协程切换
- 原子变量库的实现
- 多进程通讯方法，什么是消息队列

### 杂乱

- c++ 函数参数类型前加 const
    
    [C++ 中的 const & （常引用）参数 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/532164085)
    
    [C++函数的参数类型中为什么要加const_参数加const-CSDN博客](https://blog.csdn.net/weixin_43145361/article/details/107323400)
    
    1. 在函数内不能被修改
    2. 传参时更灵活，可以自动进行类型转换？
- 为什么 char 的范围是数值
    
    
    在 C++ 中，`char` 是一种特殊的整型数据类型，主要用于表示字符（如 `'A'`、`'B'` 等），但它的底层实际上存储的是一个整数值。这就是为什么 `char` 的范围可以表示数值的原因
    
    ### **为什么 `char` 的范围是 `128 ~ 127`？**
    
    1. **存储大小：**
        - `char` 占用 **1 字节（8 位）**，可以表示 28=256 个不同的值。
            
            28=2562^8 = 256
            
        - 默认情况下，如果 `char` 被解释为 **有符号类型（signed char）**：
            - 最高位（第 8 位）是符号位：`0` 表示正数，`1` 表示负数。
            - 其范围是：
            −27（-128） 到 27−1（127）
                
                −27（-128） 到 27−1（127）-2^{7} \text{（-128） 到 } 2^{7} - 1 \text{（127）}
                
    2. **无符号 `char` 的范围：**
        - 如果 `char` 被解释为 **无符号类型（unsigned char）**，没有符号位：
            - 范围是 0 到 255。
                
                00
                
                255255
                
        - 无符号的 `char` 常用于存储非负数或二进制数据。
    
    > 注意：标准 char 的符号性（是否 signed）是 实现定义 的，不同编译器可能有不同的默认行为。
    > 
    
    ---
    
    ### **为什么字符可以表示数值？**
    
    在计算机中，字符（`char`）本质上是通过数值来表示的。这种数值通常由字符编码标准定义，比如 **ASCII** 或 **Unicode**。
    
    ### **1. 字符的底层存储：**
    
    - 每个字符（如 `'A'`、`'B'`）都有一个对应的整数值。
    - 例如，在 ASCII 编码中：
        - `'A'` 的值是 65。
        - `'B'` 的值是 66。
        - `'0'` 的值是 48。
    - 这些整数值实际上就是存储在 `char` 类型变量中的。
    
    ### **2. 将字符和数值联系起来：**
    
    - 因为字符底层存储的是整数，`char` 类型的变量可以直接用于数值运算。例如：
        
        ```cpp
        cpp
        CopyEdit
        char c = 'A';         // 'A' 对应 ASCII 值 65
        std::cout << (int)c;  // 输出 65
        
        ```
        
    - 在代码中，我们可以通过类型转换将字符解释为其数值表示。
    
    ### **3. 常见用法：**
    
    - **字符加减：** 通过操作字符实现编码、解码等功能。
        
        ```cpp
        cpp
        CopyEdit
        char c = 'A';         // 'A' 的 ASCII 值是 65
        char nextChar = c + 1; // 加 1，变成 'B'（66）
        std::cout << nextChar; // 输出 'B'
        
        ```
        
    
    ---
    
    ### **总结**
    
    - `char` 本质上是一个 **1 字节的整数类型**，它既可以用来存储字符，也可以存储整数。
    - 字符与数值的关联来自于字符编码标准（如 ASCII），字符在底层被表示为数值。
    - `char` 的范围为 `128 ~ 127` 是因为它默认作为 **有符号类型（signed）**，而 `unsigned char` 则扩展为 `0 ~ 255`。
    
    如果你对字符编码或字符处理还有疑问，可以继续提问！