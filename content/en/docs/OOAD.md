---
title: Object-Oriented Design
slug: Object-Oriented-Design
lastmod: 2025-07-01T00:00:00+00:00
---

### **第三章 面向对象分析**

- 1.1 基本概念
    
    面向对象开发需要掌握的极为重要的能力：为软件对象分配职责
    
    方法：职责驱动的设计，遵循GRASP原则
    
    面向对象分析OOA：发现并描述问题领域里的对象或者概念（概念类）
    
    面向对象设计OOD：定义软件对象、以及它们之间如何协作完成功能的（设计类）
    
    基本过程：定义用例->定义领域模型->定义交互图->定义设计类图
    
    领域模型（概念模型、领域对象模型、分析对象模型）：问题领域的概念类以及真实对象的可视化表示
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925144946.png)
    
    低表示差异（LRG）：概念类可以作为软件类，区别是概念类没有操作，软件类有操作。就是说领域模型里面很多的概念类在我们设计的时候可以直接拿来用
    
- 1.2 面向对象分析方法
    
    系统开发有两种主要的分析方法：面向功能的分析（抽象层面）、面向对象的分析（模块层面）
    
    面向对象分析与结构化分析方法之间的最大差异是：前者根据对象划分系统，而后者根据功能
    
    面向对象分析主要步骤：识别对象 → 组织对象 → 定义对象之间的关系 → 定义对象的操作（在设计阶段完成）→ 定义对象内部细节
    
    **面向对象分析的三种方法：名词法（Conceptual model）、分析模型（Analysis model with stereotypes）、CRC cards**
    
    ### **2.1 名词法案例：**
    
    一般user ➡️ user pannel
    
    可能的抉择：一个名词，是作为概念类合适，还是作为某个类的属性更合适？
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925160408.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925160435.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925160719.png)
    
    ### **2.2 分析模型法案例：**
    
    一个健壮、稳定的模型，必须与实现环境无关，实现环境的任何变化，不会影响到系统的逻辑结构
    
    分析模型能够关注到系统的**信息、行为、展示（输入/输出）三个维度**的特性
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161243.png)
    
    分析模型用到三种符号：实体（自身的功能运算存储等）、边界（跟用户打交道输入输出）、控制类（资源调度）
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161330.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161426.png)
    
    上面废品回收机的例子：
    
    - 接口对象
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161855.png)
    
    - 实体对象
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161915.png)
    
    - 控制对象
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161934.png)
    
    ### **2.3 CRC方法标识概念类**
    
    CRC stands for：class 类、responsibilities 职责、collaborations协作
    
    CRC索引卡片格式：左边是类和职责，右边是协作类以及父类子类
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211012090225.png)
    
    CRC特点：非正式的，不是很细节的，需要进一步精化
    
    一个简单的例子：分析绘图工具软件
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211012091330.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211012093113.png)
    
    为了寻找crc我们引入了两个技术：头脑风暴，角色扮演
    
    CRC案例
    
    1.需求描述
    
    2.列出概念类
    
    3.标识核心概念类：关键的，无关的，待定的
    
    4.明确系统范围
    
    5.去掉不必要的核心类，辨析一个概念是属性还是类（它不做具体的事情，它不能改变状态）
    
    6.为核心类分配职责
    
- 1.3 面向对象设计
    
    在概念模型的基础上进行设计
    
    **低表示差异**（Low Representation Gap）：概念模型里面的概念类和设计模型里面的设计类，之间相似度很高差异很小
    
    面向对象分析的主要核心思想：**职责驱动**
    
    - 设计时考虑对象做什么、或者知道什么
    - 一个对象对其他对象承担的义务或者合约
    - 职责是一个对象的行为，而其他的对象依赖这种行为
    
    **职责定义为两类**：
    
    - 认知职责：知道自己封装的私有数据、知道你和别人相关的数据、知道哪些是可以推导出来的数据
    - 行为职责：自己可以做什么、启动其他对象做事情、控制和协调其他对象的行为
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925162902.png)
    
    废品回收机：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925214230.png)
    
- 1.4 标识概念类和对象
    
    面向对象分析的核心目的：发现对象、定义对象之间的关系
    
    为了标识领域模型里的概念，我们有三种方法：名词法、分析模型法、crc
    

### **第五章 领域模型**

- 5.1 领域模型图
    
    没有定义操作的类图
    
    包括：概念类、概念类关系、属性
    
    理解概念类的三个层面：符号、内涵、外延
    
    可以把描述性性质的概念单独作为概念类的情况：
    
    1. 在数量很大的情况，不浪费存储空间
    2. 如果删除对象的同时删除了描述，而该描述还需要继续维护
    
    构建领域模型案例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019001731.png)
    
    案例二大富翁游戏：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019002021.png)
    
- 5.2 系统顺序图 ssd
    
    把待建系统看成黑盒子，研究参与者与系统边界的交互
    
    SSD：System Sequence Diagram
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019003529.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019002900.png)
    
    系统顺序图与用例区别：
    
    在一定程度上，系统顺序图与用例描述是对应的，只是系统顺序图更精炼，用例更详细，二者互为补充
    
    系统顺序图和顺序图的区别：
    
    顺序图强调的是系统内部，对象与对象之间如何分工协作
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019003615.png)
    
    顺序图与代码
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019003735.png)
    
- 5.3 除了用例以外的需求信息
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019004341.png)
    
    分类方法一：功能性需求和非功能性需求
    
    分类方法二：FURPS+
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019004523.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019004657.png)
    

### **第六章 从分析到设计**

- 复习用例模型
    1. 参与者
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019005622.png)
    
    1. 用例
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019005745.png)
    
- 6.3 契约式设计 DBC
    
    软件的正确性可靠性
    
    design by contract
    
    specification 规格说明
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019011610.png)
    
    断言
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019011722.png)
    
    定义一个前置和后置
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019011814.png)
    
    形式化规格说明specification
    
    {P}A{Q}
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019012206.png)
    
    类不变量 class invariant
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019012525.png)
    
    **操作契约**
    
    是对用例描述的补充，强调重要的动作，其开始和结束需要一些约束
    
    后置条件：1.new对象2.与另一个对象建立联系
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019012926.png)
    
    格式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019013034.png)
    
- 6.4 开始进入设计
    
    **1.什么是架构** architecture
    
    架构是关于如何组织软件系统的一系列重大决策
    
    - 如何选择组成系统的结构元素及接口
    - 这些结构元素相互协作时的行为规范
    - 这些结构元素如何组成逐渐变大的子系统
    - 可以参考的架构风格
    
    架构也称：逻辑架构/软件架构
    
    不同于部署架构（deployment architecture）：定义这些结构元素分布在不同的物理设备上
    
    **2.逻辑架构的设计方法**
    
    分层法，  标识一定规模的结构元素 system partitioning
    
    分层架构的优点：
    
    - 各层都容易被替换
    - 较低层次包含更多的操作细节，容易成为可重用构件
    - 每层都容易分布部署与连接
    - 下层不要调用上层的功能！
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129203518.png)
    
    分层时要考虑的问题：
    
    1. 服务放在高还是低层
    2. 服务时作为应用专门的，还是通用的
- 6.5 面向对象设计
    
    **面向对象设计**主要是在领域层（domin）的每个模块（module）里面，模块与模块之间，模块与层之间的关系，不属于面向对象分析和设计的范畴
    
    面向对象设计：领域层与ui层/数据层通过特定的接口进行通信
    
    **model-view模式：**
    
    model是领域层里面做的事情，计算数据存储等
    
    view是界面，用户数据怎么传进来，怎么显示给用户看
    
    **领域对象与设计对象的一致性**
    
    领域模型中的payment是一个概念，在设计模型中是一个软件类，他们不是同一件事情，但前者启发了后者的定义，降低了表示差异
    
    **从ssd（系统顺序图）到设计**
    
    **职责驱动的设计（rdd）**
    
    设计的总体思路就是职责驱动，标识职责，并把他们分配给不同的类
    
    职责分为行为职责doing和认知职责knowing
    
    软件对象只有方法，不能说职责
    
    **GRASP原则**
    
    面向对象设计的基本原则 grasp原则
    
    通用的职责分配软件原则 general responsibility assignment software principles
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129211338.png)
    

### **第七章 面向对象设计 GRASP 原则**

- GRASP：通用职责分配软件模式
    
    GRASP，职责分配软件模式，General Responsibility Assignment Software Patterns，是面向对象设计和职责分配中的九个基本原则，最早是在克雷·拉蒙1997年的 Applying UML and Patterns 书中提到
    
    GRASP 中提到的模式和原则包括有控制器（controller）、创建者（creator）、中介（indirection）、信息专家（information expert）、低耦合性（low coupling）、高内聚性（high cohesion）、多态（polymorphism）、保护变化（protected variations）和纯虚构（pure Fabrication）[2]。这些模式都是针对软件开发上的一些问题进行解决。发明这些技巧不是为了要创造新的工作方式，而是为在面向对象设计上，旧的，经过测试的程序设计方式创建文档并且标准化。
    
- 7.1 创建者 creator
    
    由谁来负责创建这个类的新实例
    
    每项模式的格式：name、problem、solution
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129213757.png)
    
    A和B都是软件对象，不是领域对象
    
    创建模式有什么好处：对方的东西是可见的，高内聚，低耦合（我们两个一起做事情时不用跟别人创建联系）
    
- 7.2 信息专家 information expert
    
    为一个对象分配职责的一般原则，这个对象拥有完成这个职责所必须的信息
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129214705.png)
    
    information其实就是认知职责
    
    信息专家的好处：封装性encapsulation，对象充分利用自身的信息，支持低耦合和高内聚，系统行为分不到不同的类
    
    举例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129215325.png)
    
- 7.3 低耦合 low coupling
    
    如何保证设计方案的依赖性、低的变化影响度、增加可重用性
    
    **例子一 pos机计算总金额**
    
    第一种解决方案，register创建了一个对象p，然后把这个对象的参数传给sale让他去用，相当于你朋友让你装修房子，你帮他喊了个装修队，把装修队的电话发给你朋友，但是你真的有必要知道这个p的信息吗，这就增加了系统的耦合关系
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129215908.png)
    
    第二种解决方案
    
    委托 delegate
    
    register把任务委托给sale，sale去创建实例，减少了系统的耦合度
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129220149.png)
    
    **耦合**：一个元素与其他元素的连接感知以及依赖程度的度量
    
    **内聚和耦合的区别**：耦合（coupling）是模块与模块之间联系的强度，内聚（cohesion）是讲在模块内的操作之间的联系紧密的程度
    
    根据信息专家得出来的方案支持低耦合的，它自己这一个类就已经具备了必要的数据和信息，所以它在做的时候就不需要去委托别人，自己就可以完成了，这样它跟外界的交流和依赖就变少了
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129221739.png)
    
    低耦合支持类的相对独立，减少了变化带来的影响
    
    与其他原则原则放在一起考虑，不要单独考虑低耦合，类与类之间没有耦合也不好
    
    在继承关系中，子类和父类的耦合关系非常紧密。能用组合的地方不要用继承
    
    可以耦合一些稳定的框架，比如java的包和库
    
- 7.4 控制器 Controller
    
    在领域层，由谁负责首先接受并协调来自ui层的系统操作？因为ui层不应该包含任何逻辑，在ui上的系统操作必须传给领域层，由领域层来处理
    
    领域层里面有一些类应该可以代表整个系统、子系统、或者这个设备
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129222621.png)
    
    控制器有两类，一个是外观控制器，一个是会话session控制器
    
    下图第一个是外观控制器，第二个是会话控制器
    
    **外观控制器：**为子系统的一组接口提供一个一致的界面，当系统事件不是太多的时候，用一个外观控制器就可以了
    
    **会话控制器：**是虚构出来的，领域模型没有这个概念。当我这个系统事件有很多是跟用例相关的，有好几组，建议每个组定义一个handler，哪个处理销售，哪个处理退货
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129222854.png)
    
    **委托模式 delegation pattern**
    
    外部输入事件可以来自参与者或者其他系统
    
    facede相当于领域层对外部世界的脸
    
    handler处理系统某个明确的功能集合，比如相关的一组系统事件
    
    **控制器的优点**
    
    容易适应ui的变化、领域层代码易于重用，有助于保证应用所需要的操作顺序
    
    臃肿的控制器：bloated controller
    
- 7.5 高内聚 high cohesion
    
    如何使对象功能专注、可理解、可管理、同时又支持低耦合？
    
    方法：分配职责时保证高内聚
    
    这也是一种理念，不具备可操作性，用作评价工具
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129224016.png)
    
    **内聚的最佳实践：**
    
    1. 一个对象完成的功能不要太多： 谁能保证任务重的对象在完成功能时不会引用到类外部的资源呢？（增加了耦合度）
    2. 这些功能都是同一类别的
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129224534.png)
    
    **类低内聚的症状：**
    
    1. 做了许多相互无关的工作
    2. 做了太多的工作
    
    **类低内聚的原因：**
    
    1. 太粒度的抽象
    2. 做了太多本应该委托去其他类做的工作
- 7.6 多态 polymorphism
    
    如何处理依据类型不同而有不同行为的一类需求，多态原则解决的问题是在职责分配时如何避免依据类型变化而进行不同的处理
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130020311.png)
    
    多态案例
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130020633.png)
    
- 7.7 纯虚构 pure fabrication
    
    **problem：**如果依据信息专家原则获得的解决方案不合适，既不想违反低耦合、高内聚，也不想违反其他的原则，该如何把职责分配给对象（左右为难）
    
    **solution：**把高度内聚的职责分配给人为虚构出来的一个类，这个类在领域模型里没有对应的概念。
    
    这种方式在有的场合能起到支持低耦合高内聚、**重用**的效果
    
    案例
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130022331.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130022320.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106122530.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106122556.png)
    
    纯虚构原则讨论
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130022427.png)
    
- 7.8 间接 indirection
    
    若两个对象直接连接，导致耦合太近，如何解决？
    
    problem：把职责分配到哪里可以避免两个或多个对象之间的直接耦合，如何解耦对象以保持较高的可重用性？
    
    solution：把职责分配给一个中介对象，隔离对象与其他构建或者服务，使他们不产生直接耦合。因为中介对象使一种特殊的作用，一般对象与中间对象之间的直接耦合，相对比较简单
    
    和纯虚构的区别：出发点不一样，间接是为了避免直接耦合，纯虚构是在低耦合高内聚都不能满足的时候要分配一个类出来，纯虚构这个类承担的职责是相对集中的，而中介相对来说要简单一点
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130062826.png)
    
- 7.9 隔离变化 protected variations
    
    problem：需求一定会变化的，如何做到以系统的局部变化为代价就可以应对这一点。如何设计对象、系统和子系统，使得这些成分里面的变化因素、不稳定因素不会对系统的其余部分造成意想不到的影响
    
    solution：标识出能够预计的变化或者不稳定点，职责分配的时候创建一个稳定的接口能把他们与系统的其余部分隔离开来
    
    需要注意的两种可能的变化点：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130063902.png)
    
    **PV是最基本的原理**
    

### **第八章 SOLID 原则**

- 8.1 单一职责原则 SRP
- 8.2 开闭原则 OCP
    
    软件系统应当允许功能扩展（开放性）
    
    但是不允许修改原有的代码（即关闭性）
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130064901.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130064838.png)
    
    close不是绝对的，是战略性的，用到了隔离变化的思想
    
    ocp的启发：
    
    1. 定义所有的对象、数据为私有的
        
        涟漪效应 ripping effect
        
    2. 不要使用全局变量
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214081702.png)
    
    一个小例子：
    
    下面程序不符合开闭原则
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106140011.png)
    
    改变
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106140812.png)
    
    更好的方法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106140827.png)
    
- 8.3 里氏替换原则 LSP
    
    一个可以接受基类对象的地方必然可以接受一个子类对象，即凡是父类能出现的地方，子类都可以进行替换
    
- 8.4 接口隔离原则 ISP
    
    这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。它还有另外一个意思是：降低类之间的耦合度。由此可见，其实设计模式就是从大型软件架构出发、便于升级和维护的软件设计思想，它强调降低依赖，降低耦合。
    
- 8.5 依赖倒置原则 DIP
    
    dependency inversion principle
    
    依赖太重就是耦合太近
    
    ⭐️高层模块不应当依赖低层模块，两者都应该依赖抽象，高层依赖抽象层，底层也依赖抽象层
    
    ⭐️抽象不能依赖细节，细节应当依赖抽象
    
    ocp宣扬了目标，dip宣扬了一种机制
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130071031.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106135746.png)
    
    在需求发生变化时是相对稳定的
    
    启发：
    
    1. 面向接口设计，而不是面向实现设计
        
        因为抽象类和接口修改的概率低，抽象概念容纳范围广，易于扩展/修改
        
    2. 例外情况，类非常成熟稳定，再插入抽象层好处已经不多了，例如string class，这里就可以直接用具体类，不需要考虑依赖倒置
    3. 避免依赖传递性
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130072137.png)
    
    为什么面向接口设计
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106124433.png)
    
    避免依赖传递性：中间加入抽象层
    
- 8.6 迪米特法则 DP
    
    又称最少知道原则（Demeter Principle）
    
    最少知道原则是指：一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立。
    
- 8.7 命令查询分离原则 CQS
    
    The Command-Query Separation  命令查询分离
    
- 8.8 组合
    
    能用组合的地方，不要用继承
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130065625.png)
    
    **继承：**子类获得父系的全部功能，稍微调整一下，比如覆盖实现几个方法
    
    继承的副作用：
    
    1. 打破了封装性，父类和子类之间高度耦合
    2. 继承的代码时静态/编译时绑定的
    3. 客户需要购买整个软件包，花钱占内存
    4. 父类定义了许多硬性规定，难以有个性化的东西
    
    **组合：**没有打破封装性
    
    1. 对象组合是一种动态/运行时绑定
    2. 整体与部分之间只有接口边界关联，耦合较低
    3. 各部分职责明确
        
        每个对象清晰的集中在少量的任务上，容易独立测试
        
- 8.9 可见性
    
    对象之间的可见性
    对于发送者对象向接收者对象发送消息，发送者必须对接收者可见
    为了让对象 A 向对象 B 发送消息，B 必须对 A 可见。
    发送者必须有某种指向接收者对象的引用或指针
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104001135.png)
    
    实现局部可见性的两种常用方法
    创建一个新的本地实例并将其分配给一个本地变量。
    将方法调用的返回对象分配给局部变量
    

### **第九章 设计模式**

- 设计模式的定义
    
    是在软件开发中，经过验证的，用于解决在特定环境下、重复出现的、特定问题的解决方案。这些解决方案是众多软件开发人员经过相当长的一段时间的试验和错误总结出来的。使用设计模式是为了重用代码、让代码更容易被他人理解、保证代码可靠性
    
    GOF 23种设计模式有三大类：
    
    - **创建型：**单例，工厂模式，抽象工厂，原型模式，建造者模式
    - **结构型：**外观模式，适配器模式，组合模式，桥接模式，过滤器模式，装饰器模式，享元模式，代理模式
    - **行为型：**观察者模式，策略模式，命令模式，责任链模式，解释器模式，迭代器模式，中介者模式，备忘录模式，状态模式，空对象模式，模板模式，访问者模式
    
- 重构 refactor
    
    Structured method to rewrite code maintaining external behavior while applying small internal changes (transformations)
    Continuously tested with unit tests and regression tests
    Mostly for beautification
    
    在应用小的内部更改（转换）的同时重写保持外部行为的代码的结构化方法，通过单元测试和回归测试进行持续测试，主要是为了美化
    
    在保证程序语义的同时，增强结构性和可读性
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106125523.png)
    
- 9.1 单例模式
    
    **定义**
    
    这种模式涉及到一个单一的类，单例类只能有一个实例。单例类必须自己创建自己的唯一实例/对象，确保只有单个实例/对象被创建。单例类必须为外部提供了一种访问它唯一的对象的方式，可以直接访问，不需要实例化该类的对象
    
    **目的**
    
    主要解决一个全局使用的类频繁地创建与销毁的问题，节约内存。只希望有一个对象，系统所有地方都可以用到这个对象，又不使用全局变量，也不需要传递对象的引用
    
    **使用场景**
    
    WEB 中的计数器，不用每次刷新都在数据库里加一次，用单例先缓存起来。创建的一个对象需要消耗的资源过多，比如 I/O 与数据库的连接等。
    
    **创建单实例模式的方法**
    
    1. 定义私有的 private static 成员变量
    2. 定义私有的 private 构造函数
    3. 定义公有的 public static 的 getInstance 函数，用户只能通过这个 getInstance  获取实例，而不能 new
    
    ```java
    public class SingleObject {
     
       //创建 SingleObject 的一个对象
       private static SingleObject instance = new SingleObject();
     
       //让构造函数为 private，这样该类就不会被实例化
       private SingleObject(){}
     
       //获取唯一可用的对象
       public static SingleObject getInstance(){
          return instance;
       }
     
       public void showMessage(){
          System.out.println("Hello World!");
       }
    }
    ```
    
    ```java
    public class SingletonPatternDemo {
       public static void main(String[] args) {
     
          //不合法的构造函数
          //编译时错误：构造函数 SingleObject() 是不可见的
          SingleObject object = new SingleObject();
     
          //获取唯一可用的对象
          SingleObject object = SingleObject.getInstance();
     
          //显示消息
          object.showMessage();
       }
    }
    ```
    
    单实例模式的类图
    
    ![Untitled](Untitled.png)
    
- 9.2 工厂模式
    
    面向抽象编程，不要面向具体实践
    
    如果是面向接口的编程，我们可以隔离一些可能使得系统崩溃的变化。当代码需要使用很多具体的类时，增加新的具体类的时候，我们不得不修改代码。所以，我们的代码并不是“拒绝修改”的。如果要扩展新的具体类时，我们不得不重新打开代码进行修改
    
    **问题**：又想new一个对象，又不知道对象在哪里，这个对象还没产生
    
    **工厂模式的定义**：定义一个用于创建对象的接口，让子类决定实例化哪个子类。该模式把实例化延迟到其子类
    
    **GOF 定义**: 工厂方法定义了一个创建产品对象的工厂接口，将实际创建工作推迟到子类中
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214084517.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221081849.png)
    
    **核心思想**：把变化集中起来
    
    **例子**：披萨店生产不同的披萨
    
    ```
    public class PizzaStore {
    
        public Pizza orderPizza ( ) {
            Pizza   pizza = new Pizza ( );
    
            pizza.prepare () ;
            pizza.bake ();
            pizza.cut ();
            pizza.box ();
            return pizza;
        }
    }
    ```
    
    通过参数传递type，每一个Pizza的子类型都均已实现了prepare()，bake()，cut()，box() 方法
    
    ```
    But you need more than one type of pizza:
    public Pizza orderPizza ( String type) {
        Pizza pizza;
    
        if (type.equals (“cheese”)) {
            pizza = new CheesePizza ();
        } else if (type.equals(“greek”)) {
            pizza = new GreekPizza ( );
        } else if (type.equals(“pepperoni”)) {
            pizza = new PepperoniPizza ( );
        }
    
        pizza.prepare () ;
        pizza.bake ();
        pizza.cut ();
        pizza.box ();
        return pizza;
    }
    ```
    
    把上述代码改为工厂模式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214082749.png)
    
    ```
    public class SimplePizzaFactory {
        public Pizza createPizza (String type ) {
            Pizza pizza = null;
            if (type.equals (“cheese”) ) {
                pizza = new CheesePizza ();
            } else if (type.equals(“greek”)) {
                pizza = new GreekPizza ( );
            } else if (type.equals(“veggie”)) {
                pizza = new VeggiePizza ( );
            } else if (type.equals(“pepperoni”) {
                pizza = new PepperoniPizza ( );
            }
    
            return pizza;
        }
    }
    ```
    
    这里orderPizza不会再自己去new了，都交给factory去做
    
    ```
    public class PizzaStore {
        SimplePizzaFactory factory;
    
        public PizzaStore(SimplePizzaFactory factory) {
            this.factory = factory;
        }
    
        public Pizza orderPizza (String type){
            Pizza pizza;
            pizza = factory.createPizza (type); //important
            pizza.prepare () ;
            pizza.bake ();
            pizza.cut  ();
            pizza.box ( );
            return pizza;
        }
    }
    ```
    
    总结一下上面这道题的意思
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214083104.png)
    
    现在要在各个地方开分店，每个店的披萨保留老祖宗留下的操作，但允许一定的地方特色
    
    需要一种机制将所有比萨制作活动“本地化”到 PizzaStore 类，同时让 Branchs 自由地拥有自己的区域风格
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214083750.png)
    
    工厂模式的核心就是工厂函数，createPizza()就是工厂函数
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214083809.png)
    
    子类该如何确定呢？
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214084145.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105020200.png)
    
    **抽象工厂模式：**工厂模式生产一样产品，抽象工厂模式生产一系列产品，一辆汽车所需要的多种产品，前门后门
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214085129.png)
    
- 9.3 抽象工厂模式
- 9.4 外观模式
    
    目的：现有系统接口比较复杂，希望利用原有的功能重新定义新的接口。简单来说就是用新的接口实现老的功能
    
    问题：如果只希望使用现有系统的部分功能，或者以一种特殊方式与现有系统交互
    
    最小化通信， 最小化依赖
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104005323.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104005427.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104005511.png)
    
    适用性
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104005611.png)
    
- 9.5 配适器
    
    问题：当内部系统与外部第三方模块的接口不一致
    
    解决：将一个类的接口转换成客户希望的另外一个接口。Adapter模式使原本由于接口不兼容而不能一起工作的那些类可以一起工作。
    
    ```
    public interface Duck {
        public void quack ();
        public void fly ();
    }
    public interface Turkey {
        public void gobble ();
        public void fly ( );
    }
    public class TurkeyAdapter implements Duck {
        Turkey turkey;
        public TurkeyAdapter (Turkey turkey) {
            this.turkey = turkey;
        }
        public void quack ( ) {
            turkey.gobble ( );
        }
        public void fly ( ){
            for (int j = 0; j<5; j++)
                turkey.fly ( );
        }
    }
    }
    
    ```
    
    类图
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104003947.png)
    
    1. 面向抽象，不是面向实现
    2. 能用组合的地方不要用继承
- 9.6 观察者模式
    
    定义对象之间的一对多依赖关系，当一个对象改变状态时，所有依赖于它的对象都会自动获得通知
    
    观察者模式：又称publish/subscrib模式、model/view模式、source/listener模式
    
    类图
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104011019.png)
    
    案例：气象站
    
    publisher：主题对象
    
    subscriber：观察者
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220104011056.png)
    
    定义接口
    
    ```
    public interface Subject {
        public void registerObserver (Observer o);
        public void removeObserver (Observer o);
        public void notifyObservers ( );
    }
    
    public interface Observer {
        public void update (float temp, float humidity, float pressure);
    }
    
    public interface DisplayElement {
        public void display ( );
    }
    
    ```
    
    实现subject，在实现观察者模式的时候，观察者首先需要知道一个具体的主题对象，然后才能进行后续的动作
    
    ```
    public class WeatherData implements Subject {
        private ArrayList observers; //保存订阅者的列表
        private float temperature;
        private float humidity;
        private float pressure;
    
        public WeatherData ( ){
            observers = new ArrayList ( );
        }
        public void registerObserver (Observer o) {
            observers.add(o);
        }
        public void removeObserver (Observer o) {
            int j = observer.indexOf(o);
            if (j >= 0) {
                observers.remove(j);
            }
        }
        public void notifyObservers ( ) {
            for (int j = 0; j < observers.size(); j++) {
                Observer observer = (Observer)observers.get(j);
                observer.update(temperature, humidity, pressure);
            }
        }
        public void measurementsChanged ( ) {
            notifyObservers ( );
        }
    }
    ```
    
    实现订阅者
    
    ```
    public class CurrentConditionsDisplay implements Observer, DisplayElement {
        private float temperatue;
        private float humidity;
        private Subject weatherData;
    
        public CurrentConditionsDisplay (Subject weatherDataS) {
            this.weatherData = weatherDataS;
            weatherData.registerObserver (this);
        }
        public void update (float temperature, float humidity, float pressure) {
            this.temperature = temperature;
            this.humidity = humidity;
            display ( );
        }
        public void display ( ){
            System.out.println(“ Current conditions : “ + temperature + “ F degrees  and “ + humidity + “ % humidity” );
        }
    }
    
    ```
    
    什么时候用观察者模式
    
    1. 某一个对象的状态发生变化的时候，某些其它的对象需做出相应的改变 。
    2. 观察者模式定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象
    
    观察者模式的两种形式
    
    1. 推模式：能把股票价格传过来的股票机
    2. 拉模式：只是起通知作用的股票机
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105002458.png)
    
- 9.7 策略模式
    
    一个系统有许多许多类，而区分它们的只是他们直接的行为。
    
    一个类的行为或其算法可以在运行时更改。这种类型的设计模式属于行为型模式，定义一系列的算法,把它们一个个封装起来, 并且使它们可相互替换。
    
    下面是一个例子：
    
    duck自己不再fly和quack了，增加两个行为对象
    
    当需要fly的时候，委托给flyBehavior对象去处理
    
    当需要quack的时候，委托给quackBehavior对象去处理
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105011456.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105012109.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105012052.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105012544.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105012916.png)
    
    **鸭子游戏总结**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105012314.png)
    
    **策略模式**
    
    定义了算法族，分别封装起来，让它们之间可以互相替换，此模式让算 法的变化独立于使用算法的客户、
    
    这里图画错了！！不是实线，实线是继承，这里每个strategy应该是“实现关系”（虚线）
    
    组合关系是黑色的菱形
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105012831.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220105012847.png)
    
- 9.8 命令模式
    
    编程可用于控制房屋内设备的遥控器
    
    **命令模式：**将一个请求封装成一个对象，从而能以不同的请求来参数化客户对象、把所有请求存入队列或者写入日志，并且支持撤销操作
    
    各个供应商提供的on off 都有统一的接口
    
    **实现方法：**
    
    1. 命令对象中有一个通用的方法: execute()
    2. 命令对象（系统中有多个）的所有客户（remote）把每个命令对象看作是一个blackbox。当客户需要请求对象的服务时，只要简单地调用对象的虚拟execute() 方法
    
    **关键代码：**定义三个角色：1、received 真正的命令执行对象 2、Command 3、invoker 使用命令对象的入口
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221090648.jpeg)
    
    1.创建一个命令接口
    
    ```
     public interface Command  {
           public void execute ( );
     }
    ```
    
    2.创建一个请求类
    
    ```
    //由供应商提供的灯类，具有开灯及关灯两种方法
    public class Light {
      public void on () {
        System.out.println ("Light is on ");
      }
      public void off () {
        System.out.println ("Light is off");
      }
    }
    ```
    
    3.创建实现了 *command* 接口的实体类
    
    ```
    public class LightOnCommand implements Command {
          Light light;
          public LightOnCommand (Light light) {
               this.light = light;
           }
           public void execute ( ) {
                light.on ( );
           }
     }
    ```
    
    ```
    public class LightOffCommand implements Command {
            Light light;
            public LightOffCommand(Light light) {
                    this.light = light;
            }
            public void execute() {
                    light.off();
            }
    }
    ```
    
    ```
    public class StereoOnWithCDCommand implements Command {
            Stereo stereo;
             public StereoOnWithCDCommand(Stereo stereo) {
                    this.stereo = stereo;
            }
             public void execute() {
                    stereo.on();
                    stereo.setCD();
                    stereo.setVolume(11);
            }
    }
    ```
    
    4.创建命令调用类
    
    ```
    //SimpleRemoteControl 是 invoker
    
    public class SimpleRemoteControl {
           Command slot;
            public SimpleRemoteControl ( ) { }
            public void setCommand (Command command) {
                   slot = command;
            }
            public void buttonWasPressed ( ) {
                    slot.execute  ( );
            }
     }
    ```
    
    使用 SimpleRemoteControl 类来接受并执行命令
    
    ```
     public class RemoteControlTest {
          public static void main (String [] args) {
              SimpleRemoteControl remote = new SimpleRemoteControl ( );
               Light light = new Light ( );
               LightOnCommand lightOn = new LightOnCommand  (light);
    
               remote.setCommand (lightOn);
               remote.buttonWasPressed ( );
          }
    }
    ```
    
    多个按钮升级版
    
    这次遥控器将处理七个开和关命令，我们将保存在相应的数组中
    
    setCommand() 方法将一个插槽位置和一个 On 和 Off 命令存储在该插槽种，它将这些命令放在 On 和 Off 数组中供以后使用
    
    当按下 On 或 Off 按钮时，硬件负责调用相应的方法 OnButtonWasPushed ( ) 或 OffButtonWasPushed ( )
    
    ```
    public class RemoteControl {
            Command[] onCommands;
            Command[] offCommands;
    
            //在构造函数中，我们需要做的就是实例化 on 和 off 数组
            public RemoteControl() {
                    onCommands = new Command[7];
                    offCommands = new Command[7];
                     Command noCommand = new NoCommand(); //特殊的空命令。这是一种编程技巧，“哨兵”
                    for (int i = 0; i < 7; i++) {
                            onCommands[i] = noCommand;
                            offCommands[i] = noCommand;
                    }
            }
    
            public void setCommand(int slot, Command onCommand, Command offCommand) {
                    onCommands[slot] = onCommand;
                    offCommands[slot] = offCommand;
            }
             public void onButtonWasPushed(int slot) {
                    onCommands[slot].execute();
            }
             public void offButtonWasPushed(int slot) {
                    offCommands[slot].execute();
            }
              public String toString() {
                  // code here
            }
    }
    ```
    
    5.用户client
    
    ```
    public class RemoteLoader {
            public static void main(String[] args) {
                    RemoteControl remoteControl = new RemoteControl();
    
                    Light livingRoomLight = new Light("Living Room");
    
                    LightOnCommand livingRoomLightOn = new LightOnCommand(livingRoomLight);
                    LightOffCommand livingRoomLightOff = new LightOffCommand(livingRoomLight);
    
                    remoteControl.setCommand(0, livingRoomLightOn, livingRoomLightOff);
                    remoteControl.onButtonWasPushed(0);
                    remoteControl.offButtonWasPushed(0);
    }
    ```
    
    其他功能：
    
    命令可以通过实现一个撤消方法来支持撤消，该方法将对象恢复到最后一次调用 execute() 方法之前的先前状态
    
    宏命令是 Command 的简单扩展，它允许调用多个命令
    
- 9.9 组合模式
    
    组合节点 = 叶子节点 + 组合节点
    
    用一个接口处理两种不同类型的节点
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221082412.png)
    
    组合模式提供了一个结构来保存单个对象和组合
    
    允许客户端统一处理复合和单个对象
    
    组件是复合结构中的任何对象，组件可以是其他组合或叶节点
    
    图示：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221082934.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221083101.png)
    

### 设计模式的应用

- 9.6 applying
    
    **GRASP和GoF的关系**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106131553.png)
    
    非常重要的概念模型！
    
    注意，PV是最基本的原理
    
    具体的GOF模式是GRASP的具体应用
    
    **敏捷开发**
    
    ```
    敏捷原则-12条
    1 我们最优先要做的是，通过尽早、持续交付有价值的软件来使客户满意
    2 即使在开发的后期，也欢迎需求变更。敏捷过程利用变更为客户创造竞争优势
    3 经常交付可运行软件，交付的间隔可以从几个星期到几个月，交付的时间间隔越短越好
    4 在整个项目开发期间，业务人员和开发人员必须天天都在一起工作
    5 围绕有积极性的个人构建项目，给他们提供所需要的环境和支持，并且信任他们能够完成工作
    6 在团队内部，最富有效果和效率的信息传递方式是面对面交流
    7 可运行软件是进度的首要度量标准
    8 敏捷过程提倡可持续的开发速度。责任人(sponsor)、开发者和用户应该能够长期保持稳定的开发速度
    9 不断地关注优秀的技能和好的设计,会增强敏捷能力
    10 简单: 使不必做的工作最大化的艺术--- 是必要的
    11 最好的架构、需求和设计出自于 自组织团队
    12 每隔一定时间，团队会反省如何才能更有效地工作,并相应调整自己的行为。
    ```
    
    **极限编程 XP** （eXtreme Programming ）
    
    - 是敏捷软件开发中，使用最广泛的一种方法
    - XP使用面向对象方法作为推荐的开发范型
    - XP包含了 策划、设计、编码和测试 4个框架活动的规则和实践
    
    用设计模式的好处
    
    - Reuse Design 重用设计
        
        设计方案的重用比代码的重用更有意义，它会自动带来代码重用
        
    - Common Vocabulary 为设计提供共同的词汇
        
        每个模式名就是一个设计词汇，其概念使得程序员间的交流更加方便
        
    - Easy Documentation 编写开发文档更加容易
        
        在开发文档中采用模式词汇可以让其他人更容易理解设计师的想法，理解设计师为什么这么做？做了些什么？
        
    - Easy refactor 应用设计模式可以让重构系统变得容易
        
        为其他应用程序提供很好的系统架构
        
        设计模式与编程语言无关
        
    
    每一个gof pattern都是grasp原则的具体应用
    
- 9.7 统一过程 UP unified process
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106130451.png)
    
    inception、elaboration、construction、transition
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106133111.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220106133203.png)
    
- 9.8 迭代
    
    开发在迭代中进行
    
    固定长度（有时基于目标）
    
    每次迭代以测试和部分可执行文件结束
    
    每个新的迭代都建立在以前的基础上，并可能改进以前的
    
    每次迭代都以重新评估需求和可能的改进而告终
    
    每次迭代的结果是一个可执行但不完整的系统
    
    迭代的输出不是实验或一次性原型，迭代开发也不是原型设计。 相反，输出是最终系统的生产级子集