---
title: Compilers Principles
slug: Compilers-Principles
lastmod: 2025-07-01T00:00:00+00:00
---

10184602316 张彩仪

[实验存档](https://www.notion.so/40c319ce10d04572a4502c773b068005?pvs=21)

[实训题目](https://www.notion.so/e0c83c0415e646dca16e83a7a2179298?pvs=21)

### **第一章 导论**

- 编译技术的发展历史
    
    [编译技术的发展历史](%E7%BC%96%E8%AF%91%E6%8A%80%E6%9C%AF%E7%9A%84%E5%8F%91%E5%B1%95%E5%8E%86%E5%8F%B2%2009a87903ef1e4218878e1120cb447f54.csv)
    
- 编译器的各个阶段 ⭐
    
    判断编译器和编译系统
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827223455.png)
    

### 第三章 词法分析器

lexical analyzer

- 3.1 词法分析器的作用
    
    词法分析器是编译的第一阶段，主要任务是读入源程序的输入字符、将他们组成词素（lexeme），生成并输出一个词法单元（token）序列，每个 token 对应一个 lexeme，这个 token 序列被输出到语法分析器进行语法分析
    
    第一步：读一个一个的字符
    
    第二步：读进来之后把它分割成原来的合法的单词（根本的问题）
    
    第三步：合法地存下来，存在符号表 symbol table 里
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220405155612.png)
    
    **词法分析器的原理**
    
    机器和人最大的区别就是它没有前后眼，只有扫描和存储，你让他确定这是不是一个合法的单词，它很难去判断，我们必须要给到词法分析器——什么是合法的单词
    
    **正则表达式**：用来告诉机器什么是合法单词的规则
    
    **有限自动机**：告诉了机器什么叫合法的单词，机器要识别它。是一个特殊的状态转移图（Transition Diagram）
    
    **高级程序语言**：来实现自动机，实现词法分析器
    
    词法分析的三个主要元素：**Token Lexeme Pattern**
    
    Token 是一组常见字符串的分类，Pattern 是 Token 形成的规则约束；Lexemes 是实际的源程序里的字符序列，和某个 token 模式匹配，并被词法分析器识别为该 token 的一个实例；还有一个属性叫 Attributes 这个东西在词法分析器里没用，是用于语法分析器的
    
    设计token表的时候要根据实际情况，不是唯一的，比如可以用 if 这一个元素作为单独的 token，也可以像 relation 以集合作为一个 token
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220509161740.png)
    
    下面是Token 的简单分类，在很多程序设计语言中，这些类别覆盖了大部分或所有的 token。分类的原因是要有一个简单的规则能把各种各样的 token 说请楚，只有分类才能让每一类的规则说明变得简单
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220405161321.png)
    
- 3.2 词法单元的规约
    
    ### **串和语言**
    
    Alphabet：一个有限的符号结合，例如ASCII、unicode
    
    String：该字母表中符号的一个有穷序列
    
    Language：某个给定字母表上一个任意可数的 string 的集合。根据这个定义，像空集、进包含空串的集合、所有语法正确的英语句子、所有语法正确的C程序都是语言
    
    Prefix：前缀，从 s 的尾部删除 0 个或多个符号后得到的串
    
    Suffix：后缀，从 s 的开始处删除 0 个或多个符号后得到的串
    
    Substring：子串，删除 s 的某个前缀和某个后缀之后得到的串
    
    Subsequence：从 s 中删除 0 个或多个符号后得到的串，被删除的符号可能不相邻
    
    ### **语言上的运算**
    
    语言有两个本质：有规则、无限可扩展
    
    在词法分析中，最重要的语言运算是 **并、连接、闭包**，可以用有限的算子，扩充为无限的语言
    
    **结构归纳法**：指用有限的算子，扩充为无限的语言这种方法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220405194558.png)
    
    感受一下运算的例子
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220405194854.png)
    
    ### **正则表达式**
    
    正则表达式是一种用来描述 lexeme 模式的重要表示方法，高效描述在处理 token 时要用到的模式类型
    
    首先要有字母表，然后用并、连接、闭包这些运算符来描述标识符
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220421235938.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422000116.png)
    
    正则表达式特殊符号说明如下：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422003534.png)
    
    正则表达式的特征表：
    
    值得注意的是 r* * = r*，克林闭包的克林闭包就等于克林闭包
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422000407.png)
    
    正则表达式的一些举例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422000238.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422000628.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422001048.png)
    
    ### **扩展：正则定义**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422003604.png)
    
- 3.3 词法单元的识别
    
    ### **状态转换图**
    
    状态转移图的目的是用来运行正则表达式
    
    状态转移图的定义：状态、动作、开始状态、结束状态
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422004311.png)
    
    每个状态转移图是确定性的，无需在两种不同的操作之间进行选择
    
    例一：一个识别大于等于的 transition diagram。圆圈0表示开始状态，双圆圈7和8表示结束状态
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422005143.png)
    
    例二：一个识别各种关系符号的 transition diagram。终止状态表示此刻计算机有能力识别出这个符号了的时候，就可以结束了
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422005314.png)
    
    例三：一个识别空格的 TD 和一个能识别标识符的 TD
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220422005702.png)
    
    为什么要到30才终止而不是29呢：因为机器没有前后眼，只有识别到了other其它字符才知道它识别完了，是一种机器的思维
    
    下面这三条规则是机器不确定的，到底是无符号数还是小数还是第三个呢，机器只通过第一个字符它是不知道的。在没有引入子集构造法的时候，我们就可以强行给机器指定一条（最长的）的开始，把不确定性变成确定型
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220428224215.png)
    
- 3.4 有限自动机 ⭐ = 确定型自动机（DFA） + 不确定性自动机（NFA）
    
    有限自动机：有有限个状态，词法分析器里用的状态转移图是有限自动机
    
    有限自动机可以分为确定型自动机（DFA）和不确定性自动机（NFA）
    
    不确定性自动机（NFA）：1. 有几个可选项 2. 不确定性自动机的性质是空间占的少，速度很慢 3. 很容易表示正则表达式，但不太精确
    
    确定型自动机（DFA）：1. 看到一个字符之后就明确的知道在哪里 2. 不用回溯，速度会非常快 3. 需要更高的复杂性来表示正则表达式，但提供更高的精度 4. 词法分析器的最终目的，就是构造DFA
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220428233332.png)
    
- 3.5 不确定型自动机 NFA
    
    ### **不确定型自动机 NFA**
    
    一个不确定的有穷自动机由以下几个部分构成
    
    - 一个有穷的状态集合 S
    - 一个输入字母表 input alphabet
    - 一个转换函数 transition function/move
    - 开始状态和终止状态
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220428234314.png)
    
    和确定型自动机的唯一区别就是，从此时这个状态，要么识别一个动作，要么什么都不做识别空，就可以到达接下来的状态集合，体现了不确定性。下一个动作可以到达这个状态，也可以到达另一个状态，也体现了不确定性
    
    不确定型自动机举例
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220428235056.png)
    
    还有另外一种自动机表示方式叫做 transition table，但是在表中一定要注明开始和结束状态
    
    其实图和表都可以，下面是两种表示方式的举例
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220428235521.png)
    
    练习：根据正则表达式画一个不确定型自动机，每个人画出来可能都不一样
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220428235730.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220428235840.png)
    
- 3.6 确定型自动机 DFA
    
    ### **确定型自动机 DFA**
    
    确定型自动机就是把不确定自动机加上两个约束
    
    - 动作不能为空，空转移不存在
    - 每个动作只能到达唯一的下一个状态
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429000142.png)
    
    定义token的正则表达式，然后转化为 DFA——**词法分析器的最终目的**就是获得我们构造出来的 DFA
    
    一张图感受，为什么一定要先转换成 NFA，再转化成 DFA。因为我们很容易把一个正则表达式写成 NFA，不太容易直接写成 DFA，看起来就很复杂
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429000525.png)
    
- 3.7 Thompson构造法 RE - NFA
    
    ### **Thompson构造法 RE - NFA**
    
    构造方法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430133908.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430133926.png)
    
    构造连接的时候有两种方法，这是唯一的不确定性
    
    上图是经过优化过方法，下图是连接的两种方法扩展：
    
    构造流程，先识别后合并
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430135231.png)
    
    Thompson构造法的特点
    
    - 状态数量可控，不一定是最少
    - 只有唯一的一个开始状态和一个结束状态
    - 最多只有一条输出的有意义的边，和最多两条输出空串的边
    - 注意做题规范：从零开始，从左至右，从上至下标状态
    
    Thompson构造法的例题一      **(a|b)*a**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430140623.png)
    
    Thompson构造法的例题二     **(ab*c) | (a(b|c *))**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430141417.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430141537.png)
    
    最后的结果，这个算法看起来挺好玩的，像拼乐高一样，不难
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430141602.png)
    
    对NFA和DFA进行比较：
    
    NFA 有很多不确定的选择，所以在时间上会慢一些
    
    DFA 状态数目会比较大，但是时间肯定会小
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430142741.png)
    
- 3.8 子集构造法 NFA - DFA
    
    ### **子集构造法 NFA - DFA**
    
    *子集构造法是这一章最难的方法*
    
    子集构造法的核心思想：消除空串，消除多种可能
    
    **构造法方法总结如下：**
    
    1. 找出从该初始状态出发，仅通过e移动能够到达的所有状态
    2. 每出现一个新的子集闭包，标记为一个新的状态
    3. 并且分析由这个新状态分别输入 a和b 会生成什么样的子集
    4. 如果生成的这个子集是以前的，就不用管，如果是新的，回到步骤2
    5. 直到不产生新的状态为止
    
    例题：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429005212.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429005238.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429005256.png)
    
    S0是开始状态，S4是结束状态
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429005311.png)
    
    下面是练习一
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429005336.png)
    
    练习的答案
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429005355.png)
    
    下面是练习二
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220429005412.png)
    
- 3.9 直接构造法 RE - DFA
    
    ### **直接构造法 RE - DFA**
    
    首先要进行准备工作：
    
    - 对正则表达式需要加一个特殊的符号，标注表达式结束了
    - 为了避免重复，给所有的字符重新标号
    
    followpos(i) 函数：可能跟在这个字符后面的字符集合，i 代表的是标号
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430150214.png)
    
    举个例子
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430150249.png)
    
    机器想得出followpos还需要另外三个辅助函数，函数的n代表的是
    
    - firstpos：一个子串有可能出现在第一个的那个位置所对应的标号，的集合
    - lastpos：一个字串有可能出现在最后的那个位置所对应的标号，的集合
    - nullable：布尔集，是否有可能为false
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220430150344.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829084404.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829085113.png)
    
- 3.10 DFA的最小化
    
    ### **DFA的最小化**
    
    例一：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828222211.png)
    
    例二：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828222242.png)
    

### **第四章 语法分析**

- 语法分析简介
    
    词法分析器的主要目标是**看一个 token 是否合法**，流程是
    
    1. 先给定规则比如正则表达式
    2. 表达为计算机可以识别的 DFA
    
    语法分析器的任务是**看一个句子是否合法**，按照词法分析器的流程可以总结出
    
    1. 定义什么叫一个句子
    2. 用什么样的方式写这个规则（上下文无关文法：1. 便于被计算机识别和认可 2. 是正则表达式的一种扩展）
    3. 实现计算机能够解决的一个 transition diagram 的形式（语法树）
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827145617.png)
    
    语法分析方法的分类：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827145617.png)
    
- 4.0 句子句型和语言
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827145305.png)
    
- 4.1 错误处理
    
    一个编译器的好坏很大程度取决于你的错误处理
    
    观察下面程序的错误
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220405201802.png)
    
    错误处理的步骤：发现错误、发现错误所在的位置、描述错误、修正错误
    
    两种错误处理的方法：
    
    **Panic Mode** 快速发现非常确定的错误之后快速解决，比如少了分号
    
    **Phrase Level** 前后看一看就能发现缺了什么
    
    **Global correction** 全局修改
    
- 4.2 上下文无关文法 CFG
    
    content-free grammar
    
    ### **正式定义**
    
    一个上下文无关文法由终结符号、非终结符号、一个开始符号、一组产生式组成
    
    **终结符 T**：也指 token，是词法分析器输出的词法单元的第一个分量
    
    **非终结符 NT**：表示串的集合的语法变量
    
    **开始符 S**：其中的一个非终结符号，表示的串集合就是这个文法生成的语言
    
    **产生式 PR**：描述了将终结符号和非终结符号组成串的方法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220405222612.png)
    
    例如在下图中 E 是非终结符号，+ - * / id num ()  都是终结符号， E 也是开始符号
    
    箭头后面表示的是产生式，第一行包括了五个产生式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220405222122.png)
    
    一些判断技巧：只要在左边出现的就是非终结符，凡是没有出现在了右边的就是常量（终结符），一般将第一个产生式出现的第一个非终结符指定为开始符
    
    ### **推导**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411204644.png)
    
    如图最后一个式子，id+id 已经没有 **非终结符** 在里面了，就是已经停止替换了，就可以称为一个句子（sentence），中间的形式被称为句型（sentential form）
    
    最左推导
    
    最右推导
    
    ### **语法树**
    
    怎样从上下文无关文法产生语法树？
    
    语法树是我们计算机能够自动识别的 transition diagram 的一个形式
    
    两种表示方法：推导法和表示法，对计算机来说没什么差别
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411221115.png)
    
    ### **二义性**
    
    用最左推导推一下
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411221430.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411221501.png)
    
    例子二，再试试用最左推导，依然可以推出来
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411221702.png)
    
    但其实里面有值得注意的问题，为什么第一步选了 E+E 而不是 E * E，当我们第一步选用 E * E 来替换，发现结果仍然是一样的。所以当我们在这么确定的规则下还是有很多不确定，这就是我们说的二义性
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220509184939.png)
    
    二义性：有两个不同的最左推导或者有两个不同的最右推导（而不是说有两个不同的推导），这样的文法叫做二义性文法，有歧义。举例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411222502.png)
    
    什么样的文法是受欢迎的：1. 没有二义性 2. 不存在左递归 3. 没有公共因子的
    
    **消除二义性**
    
    规定优先级，乘法的优先级大于加法，并且从左至右也是优先级
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411222837.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220509185415.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220509185442.png)
    
    ### **左递归**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411223255.png)
    
    左递归又分为一眼可以看出来的（直接左递归）和一眼看不出来的（间接左递归）
    
    **消除直接左递归的方法：**
    
    引入一个A’，A相当于 beta开头，中间有无数个 alfa，最后是A‘
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411223633.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411223756.png)
    
    消除左递归方法的例子：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411224022.png)
    
    **消除间接左递归的方法：**
    
    间接左递归举例
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411224228.png)
    
    1. 把所有的非终结符随便排个序
    2. 循环，判断该非终结符有没有直接左递归，没有就下一个
    3. 把在它之前的非终结符都替换掉
    
    一个例子：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411225032.png)
    
    ### **公共左因子**
    
    解决方法：推迟做选择
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220411231251.png)
    
- 4.3 自顶向下语法分析
    
    CFG的三个约束：二义性，左递归，左公共因子
    
    ### **递归向下 recursive-descent parsing**
    
    就是实现不对二义性，左递归，左公共因子做预处理，等到过程中出问题了再回溯，回溯以后再进行另外的选择，要提前制定不确定选择的规则。不高效
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425191837.png)
    
    ### **可预测 predictable parding**
    
    先预处理（两步：消除左递归和提取左因子），对上下无关文法实现约束，没有回溯比较高效
    
    ### **LL(1) Stack Implementation ⭐️**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828091037.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828091222.png)
    
    LL(1) 是最经典的自顶向下语法树
    
    第一个L表示输入从左至右扫描，第二个L表示输出是一个最左推导，(1)表示指针一次只看一个字符
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425193310.png)
    
    输入：字符串加规定的end mark
    
    输出：是一个语法树，一系列有序的产生式或推导规则，说明第一步、第二步....分别用的什么规则
    
    栈：用栈来重写规则，储存过程
    
    语法表：让机器知道遇到了这个字符，就知道要使用哪个规则。行数是非终结符，列数是终结符加 $ 符(end mark)，表格里填了的内容是产生式
    
    **STAKE的步骤详解**
    
    首先在栈里放一个end mark和开始符S
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425194235.png)
    
    下面是一道简单的例题
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425194755.png)
    
    然后就可以很顺利的推导出语法树
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425195257.png)
    
    再看一道稍微难一点的例题
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425195409.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425200018.png)
    
    这里第一步没有output，因为第一步还是静止状态。其实两种写法都可以
    
    **TABLE步骤详解**
    
    主要的函数
    
    - FIRST 不仅仅是终结符一定出现在里面的，是说有可能会出现的，注意空也要在 FIRST 里面
    - FOLLOW 有可能跟在它后面的字符的结合
    
    如何算first集合
    
    1. 先算alpha，就是右边一列的first集，把第一个字符是终结符的写出来，是非终结符的暂时写不出来
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425211543.png)
    
    1. 开始算非终结符的first集合，就是它的两个生成式的first集合的并集
    2. 通过非终结符的first集合，可以算出以这个非终结符开头的alpha的first集合，比如下面的 FIRST(F) 算出来之后就可以算 FIRST(FT‘)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425211910.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425212241.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828090547.png)
    
    再介绍一个有顺序一点的分析方法，不像上面那么乱七八糟
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425212419.png)
    
    如何计算 follow 集合的方法，follow集只看非终结符！
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425225929.png)
    
    举个简单例子看看
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425230610.png)
    
    注意：如果跟在 X 后面的字符的 First 集有空集，则要把产生式左边这个非终结符的 Follow 集也都放进来，比如底四五条的 F
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425230650.png)
    
    知道了 FIRST 和 FOLLOW 这两个集之后，做这个表格就变得非常简单了
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220425231024.png)
    
    下面也看一个例子
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828093707.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828093722.png)
    
    ### **LL(1) 文法的特点**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828084055.png)
    
    1. 不可能开始于两个相同的terminal集合，如果有公共左因子，则一定不是 ll1文法，否则在表单里面会有两个或两个以上的产生式供选择
    2. 不可能两个都为空，至多只有一个
    3. 如果 b 为空，则 a 不可以以任何 follow(a) 里面的terminal 开头
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823210947.png)
    
    **举例，**硬着头皮把表做出来，发现有二义性，所以就知道了不是 ll1
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823211657.png)
    
    **练习题：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823212328.png)
    
    首先，预处理，消除左递归，对于直接左递归就是新增加一个终结符
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823212501.png)
    
    计算 first 和 follow 集合
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823212640.png)
    
    结论不是唯一的，1. 如果没有对它做预处理，然后判别出有问题的，就不是ll1文法 **（所以只要存在左递归，就可以判断出不是 LL1 文法）**2. 如果是做了预处理，和之前的文法是等价文法，经过预处理的文法判别出没问题，就说明经过预处理之后的文法是 ll1 文法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823213545.png)
    
    ### **LL(1) 错误处理**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828091354.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828092356.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828092547.png)
    
    举例：检测 aab 是不是合法
    
    第一列第四行的时候，a和b对上了，就运行不下去了，可以选择去掉 b
    
    第二列第四行的时候，A遇到e，运行不下去了，选择去掉把A e a 都去掉
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823215222.png)
    
    错误处理的方法总结：后面两个几乎不会用
    
    1. 抛弃字符
    2. phrase level 前后文观察
    3. 硬生生的构造产生式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823221712.png)
    
    ### **总结**
    
    topdown只是一种分析方法，之所以要先将是因为太直观了
    
    bottomup的方法不那么直观，但是解决了topdown的一个弊端/局限性，原因就在于构造parsing table的时候想的太简单了
    
- 4.4 自底向上语法分析
    
    自底向上：从叶子节点出发，倒着回去找到根节点
    
    ### **Shift Reduce Parsing**
    
    一个规约 reduction 过程的（最右推导的反过程）举例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823224339.png)
    
    **shift-reduce parsing 过程：**
    
    1. shift 知道哪一部分是可以规约的
    2. reduce 开始进行规约
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823231552.png)
    
    **有哪些分析方法：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823233048.png)
    
    SLR 最简单，LR最复杂，LALR 是介于中间的也是最常用的
    
    ### **Handle 句柄**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828094457.png)
    
    常考题：句子 句型 句柄的区别
    
    句柄：字符串句柄是匹配产生式规则右侧的子字符串，但是匹配了产生式右侧的不一定是句柄
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823230832.png)
    
    从人类和电脑的角度来说，自底向上都是不容易理解的。所有问题都可以被归结为找句柄的问题
    
    怎么找句柄，下面红色的部分就是句柄
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823231316.png)
    
    ### **LR文法和LR(k)分析法**
    
    **什么是 LR 分析法**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828094222.png)
    
    **栈方法实现：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823232612.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823235434.png)
    
    1. 如果 stack 里面没有句柄，则从 input 里面弹出到 stack
    2. 如果 stack 里面是句柄，找action来规约
    3. action 除掉 shift，倒过来输出，就是整个过程
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823232031.png)
    
    和LL的区别与联系：
    
    1. 框架是一样的，用了栈还有一张神秘的表
    2. 分析的过程稍微有点不同
    3. 更大的不同在于这张表
    4. LL1 和 LR 的方法哪个好？答案是 LR（表达能力的比较，能用 LL1 分析出来的语法一定能用 LR 分析出来，所以 **LR 的表达能力更强**，适应更多的范围）
    
    ### **LR(0) Item / 增广文法 / 项目集闭包**
    
    **什么是 LR(0) Item：**一个 item 表示他可能的状态有多少个
    
    **扩展文法 S‘ -> S**：看似没有用，但是代表了整个分析的开始和分析的结束
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825005225.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828103236.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828103441.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828103547.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828103906.png)
    
    ### **LR(0) 分析**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220823235434.png)
    
    再看这个过程，其实是需要两张表，那纵坐标 states 指的是什么？这个过程的难点就在于这个 state
    
    什么是configuration：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825001551.png)
    
    左边 stack 里面 S 是非终结符序列，X是该非终结符的状态序列，不管是pop出来还是规约进去都应该是成双的：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825003021.png)
    
    所以再回头看这个表
    
    - goto table 主要目的就是当我规约到了这个非终结符，我要给它什么样的状态信息
    - action table 里面
        - s 表示 shift，s5 是成对的属性（动作+状态id）
        - r 表示 reduce，动作是 pop，不同的是 r2 表示（动作+左边产生式的序号，表示用哪一个产生式进行规约）
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825003051.png)
    
    ⭐️查表的过程：
    
    查表的结束情况是查到了 accept
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825004455.png)
    
    ### **LR(0) 制表**
    
    这里依然需要两个算法 ：
    
    **1.闭包算法**
    
    - 自身在里面
    - 把将要分析的非终结符的产生式也放进来
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825165608.png)
    
    一个闭包运算的例子：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825170129.png)
    
    **2.Goto算法**
    
    就是goto E的闭包就相当于 E后面有黑点的状态的集合
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825170430.png)
    
    运用上面两个算法计算 collection：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825222813.png)
    
    然后就会恍然大悟：这里构造出来的 I0 - I11 就是之前那张表的纵坐标的是一个状态。所以状态数就是来自于我通过 I0 做所有的 goto 函数，不会产生新的 item 集合了，那此时就做完了，找到了所有的状态数
    
    终于讲到了构造 SLR parsing table 的步骤了 .......
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825223743.png)
    
    1. 我们要构造 G 的语法树，首要的一点就是要扩展语法 G’！
    2. 找到所有的状态集，也就是 collection
    3. 构造 action table，横坐标就是终结符和 $ 符
    4. 构造 goto table，横坐标的项就是非终结符
    
    所以再回顾一下这张表就是由这种方法构成的：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825224437.png)
    
    再做一个例子：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828104757.png)
    
    **SLR grammar 的特点**
    
    SLR 是无二义性的，但是不是所有无二义性的语法都可以用 SLR 来解决，毕竟功能还没有那么强大
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825224548.png)
    
    ### **LR(0) 冲突**
    
    只有两种冲突会出现， shift/shift 冲突是不会出现的，因为指针一次只指向一个
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825224716.png)
    
    一个冲突的例子：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825225059.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825225347.png)
    
    但是这个冲突2的情况 LL1 是能做的
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825225456.png)
    
    产生冲突的原因就是follow集合出了问题，因为要把 follow 集里面的所有都拿来规约，如果有一个规则来告诉计算机遇到什么就用哪个规约就好了
    
    ### **SLR(1)**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828110855.png)
    
    在状态2的 B T规约冲突中，通过查询 B T 的follow集可以得出，当2遇到B的follow集元素 d 时，采取4号产生式规约， 当2遇到T的follow集元素 ￥ b 时，采取42产生式规约
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828111412.png)
    
    以前是全部都规约，现在是遇到 follow 集里面的元素才规约
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828111737.png)
    
    ### **SLR(1 )冲突**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828111908.png)
    
    ### **LR(1)**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828114852.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828115054.png)
    
    引入 LR1 Item 的概念，跟 LR0 Item 的区别：就是多了一个最后的 a 字符
    
    作用：为了解决 SLR 的冲突
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825230907.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828122215.png)
    
    构造 collecton 的方法和 LR0 Item 构造 collecton 的方法如出一辙，依然要使用闭包和 goto 方法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825231125.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825231238.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825231300.png)
    
    简写说明：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825233122.png)
    
    **LR1 Parsing Table 的构造：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825233734.png)
    
    **例子一：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825233634.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825233821.png)
    
    例子二：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828123543.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828123704.png)
    
    **一个很容易很容易出错的例子：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825235806.png)
    
    观察一下画线的这些有什么不一样
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825235913.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220825235930.png)
    
    ### **LALR(1)**
    
    是前面两种方法的优化，既解决冲突，又可以减少状态数目
    
    它是仿照 LR 做的，但是最后状态数目可以跟 SLR 一样多
    
    但是表达能力不能跟 LR 相比，因为在合并状态的过程中损失了一些准确性
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826000059.png)
    
    什么是同心核 core
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826002323.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828124019.png)
    
    LALR 分析的基本思想：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828124919.png)
    
    **构造 LALR parsing table 的方法：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826002236.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828125123.png)
    
    ### **LALR(1) 冲突**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828125233.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828125652.png)
    
    ### **Operator Precedence Parsing**
    
    ### **总结**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826002428.png)
    

### **第五章 语义分析**

- 5.1 语义分析简介
    
    编译原理前端：词法分析、语法分析、语义分析
    
    语义分析：了解每一行语句的含义
    
    有哪些语义分析器：
    
    1. 属性文法
    2. 语法树的构造
    3. 自顶向下
    4. 递归分析
    5. 自底向上
    6. 类型检测
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826214840.png)
    
    对比：词法分析、语法分析、语义分析
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826215157.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826215327.png)
    
    **语法制导翻译：**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828150345.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828150530.png)
    
    之前提到的 token 那几个元素，唯独 attribute 是告诉你这个token具有什么样的意义
    
    语义分析可能会做的一些事情：
    
    1. 生成中间代码
    2. 把信息放到符号表里
    3. 类型检查 等等
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826215556.png)
    
    **语法制导定义和翻译模式**
    
    语法制导定义：用来定义语义规则的
    
    翻译模式：如何使用这些语义规则，就是使用语义规则的定义
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826220410.png)
    
- 5.2 语法制导定义 SDD
    1. 就是上下文无关文法的一个扩展形式
    2. 属性分为综合属性和继承属性
    3. 每个产生式都携带一系列的语义规则
    4. 语义规则（semantic rules）依赖于属性之间的关系
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826220752.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828150715.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828151108.png)
    
    正式定义：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826222358.png)
    
    **语法制导定义举例：**
    
    语法制导定义 = production + semantic rules
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826222513.png)
    
    这里的属性都是综合属性，这个过程是一个从底向上的过程：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826224422.png)
    
    再看一个继承属性的例子：
    
    1. L.in 算的是产生式右边的某一个元素 L 的属性，那么毫无疑问 in 是一个继承属性，从第一条规则暂时判断不出来 type 是什么属性
    2. 从第二条和第三条可以看出 type 是产生式左边的非终结符的属性，是典型的综合属性
    3. 第四条的写法要注意不要写成 L.in = L1.in 了，如果是这样 in 就是综合属性了，在计算机里面一个属性不可能既是继承属性，又是综合属性
    4. 第五条的意思是 L.in 的属性是来自 id 的
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826224549.png)
    
    依赖图：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826225453.png)
    
    ### **注释语法树**
    
    每个节点都带有属性值的树叫做注释分析树：
    
    1. 在每个节点都可以显示属性的值
    2. 叶子节点的值是词法分析器里面 source code 自带的
    3. 内部节点是通过语义规则一步一步算出来的
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826224135.png)
    
    注释树举例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826224101.png)
    
    ### **依赖图**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828154656.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828155433.png)
    
    在原来语法树的基础之上，希望能够构造出来它的属性计算的那个关系，所以就画出了红色的部分，**综合属性比继承属性好，继承属性看起来没规律，不好算，综合属性看起来有规律，好算**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827131925.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827143518.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827144020.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827144520.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827144142.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827144312.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826225637.png)
    
- 5.3 属性文法
    1. 每一个symbol后面带有一系列的语义属性
    2. 每一个产生式后面带有一系列的语义规则
    3. 一个属性文法是带有语义属性和语义规则的上下文无关文法（CFG）
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826223634.png)
    
    ### **综合属性和继承属性**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828151437.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828151525.png)
    
    ### **S属性文法 S-Attribute**
    
    特点：
    
    1. 只有综合属性的属性文法
    2. 可以按照语法分析树节点的任何自底向上的顺序来计算它的各个属性值
    3. S属性文法可以在自底向上的语法分析过程中实现
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220826230217.png)
    
    结合SLR进行语义分析的举例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827230117.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827230220.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827225458.png)
    
    慕课：
    
    在规约的时候同时完成属性计算
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827192224.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827192541.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827192822.png)
    
    ### **L属性文法 L-Attribute**
    
    特点：
    
    1. 在一个产生式所关联的各属性之间，依赖图的边可以从左到右，不能从右到左，所以在依赖图中一般把综合属性放在节点的右边，继承属性放在节点的左边
    2. 既包含综合属性，又包含继承属性，但是继承属性被严格限制
    
    限制条件：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827225635.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827193111.png)
    
    判断是不是L-属性文法：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827225956.png)
    
    Q的属性 in 依赖于 R 的属性了，所以这不是一个L属性文法
    
- 5.4 翻译模式 SDT
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828150907.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828150933.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827194518.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827195246.png)
    
    ### **S属性文法的SDT**
    
    把S属性文法转换为翻译模式，将每个语义动作都放在产生式的最后
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828161008.png)
    
    用LR语法分析实现：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828161110.png)
    
    扩展的LR语法分析栈：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828161503.png)
    
    例如：在自底向上的语法分析中实现桌面计算器
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828161836.png)
    
    ### **L属性文法的SDT**
    
    把L属性文法转换为翻译模式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828161920.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828170921.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828171027.png)
    
    ### **设计翻译模式**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827195418.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827195532.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827195938.png)
    
    翻译模式举例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827201342.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827201609.png)
    
    写成翻译模式：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827201759.png)
    
    ### **翻译模式的使用**
    
    下面是一个把中缀变成后缀的例子：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829074642.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829074652.png)
    
    ### **在非递归的预测分析中进行翻译**
    
    ### **在递归的预测分析中进行翻译**
    
    ### **L属性定义的自底向上翻译**
    
    ### **消除翻译模式中的左递归**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827202535.png)
    
    真他妈看不懂啊
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827203414.png)
    
    妙啊，这个图看懂了
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827203913.png)
    
    方法总结
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827210125.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827210354.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827210711.png)
    
    ### **L属性文法改写嵌入式的 SDT 采用自底向上的方法**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829082600.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829082632.png)
    

### **第七章 运行时环境**

- 怎么设计和构造这个环境
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828174759.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828175546.png)
    
- 运行存储分配
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828181056.png)
    
    、
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828181406.png)
    
    过程的定义：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828181508.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828181613.png)
    
- 静态存储分配
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828181703.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828181746.png)
    
    常用的静态存储分配方法：顺序分配法和层次分配法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828181915.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828182055.png)
    
    层次分配算法：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828182153.png)
    
- 栈式存储分配
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828182248.png)
    
    活动树的概念：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828182354.png)
    
    以快排为例：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828182505.png)
    

### **第八章 中间代码生成**

- 中间语言的特点和作用
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827211523.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827211552.png)
    
- 后缀式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827211831.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827212248.png)
    
- 有向无环图 DAG
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827212357.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827212528.png)
    
- 三地址代码
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827213151.png)
    
    对这个树做自下而上，从左到右的遍历，就可以把这个抽象语法树转换为三地址代码
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827213226.png)
    
    有向无环图构成的代码少了两条指令，因为它消除了公共的冗余的子表达式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827213356.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827213554.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827213702.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827213743.png)
    
    复杂的三元是
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827213847.png)
    
    三元式的缺陷：如果要删除增加语句，或者是要调整语句的顺序，都可能要改变某些语句的位置下标，于是出现了间接三元式
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827221251.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827221402.png)
    
- 三地址代码的算法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829011613.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829011813.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829011940.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829012222.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829012803.png)
    
- 三地址算法的语义制导翻译
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829013923.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829013938.png)
    
- 构造符号表
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220829015245.png)
    

### **复习课**

- Todo list befor exam
    - [x]  学习SLR LR LALR 的算法
    - [x]  看哈工大慕课的语法制导的内容
    - [x]  迅速看张敏的后几章的录屏
    - [x]  做去年和前年的试卷，查漏补缺
    - [x]  做大夏学堂上的练习题
    - [x]  过程中不懂的就去做混子必备里面的题
    - [x]  复习第三章
    - [x]  混子必备其他题型的解法
    - [ ]  张敏课上说的那个必考题
    - [ ]  看龙书第一章的概念
    - [ ]  看龙书第七章的概念
    - [x]  三地址算法
    - [x]  小纸条
    - [ ]  把属性文法那章的作业打印下来

第一章考概念多：判断编译器和编译系统，编译器各个阶段的分组

重点在3-6章，词法、语法、语义：

次重点在7-8章，运行时环境、中间代码生成：作为编译时候的运行时环境，你应该清楚的了解，你这个运行时环境的基本构造，应该包含哪部分，第七章建议一字一句的去读

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827221916.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827221943.png)

第八章只讲了三地址代码

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827222008.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828175816.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220828175846.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220827102013.png)

计算题：九大算法和三地址代码一共十种类型

简答题：小型算法，左递归，找句柄，预处理等等，就是一些实施细节。一段话，比如我要不要做二义性处理，这种简单的分析

选择题和填空题都是考核心概念：第一章第七章