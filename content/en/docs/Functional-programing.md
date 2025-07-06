---
title: Functional Programing
slug: Functional-Programing
lastmod: 2025-07-01T00:00:00+00:00
---


# **一、BASIC**

## **1.1 数据与函数**

### **枚举类型**

Inductive 定义一个数据集合

```
Inductive day : Type :=
  | monday
  | tuesday
  | wednesday
  | thursday
  | friday
  | saturday
  | sunday.
```

Definition 可以写一些操作函数

```
Definition next_weekday (d:day) : day :=
  match d with
  | monday ⇒ tuesday
  | tuesday ⇒ wednesday
  | wednesday ⇒ thursday
  | thursday ⇒ friday
  | friday ⇒ monday
  | saturday ⇒ monday
  | sunday ⇒ monday
  end.
```

在 Coq 中检验的方式一共有三种：

第一，用 Compute 指令来计算包含 next_weekday 的复合表达式

```
Compute (next_weekday friday).
Compute (next_weekday (next_weekday saturday)).
```

第二，将期望的结果写成 Coq 的示例

```
Example test_next_weekday:
  (next_weekday (next_weekday saturday)) = tuesday.

Proof. simpl. reflexivity.  Qed.
```

这段代码基本上可以读作“若等式两边的求值结果相同，该断言即可得证”

第三，我们可以让 Coq 从 Definition 中提取出用其它更加常规的编程语言编写的程序

### **布尔值**

```
Inductive bool : Type :=
  | true
  | false.
```

布尔值的函数可按照同样的方式来定义

```
Definition negb (b:bool) : bool :=
  match b with
  | true ⇒ false
  | false ⇒ true
  end.
```

```
Definition andb (b1:bool) (b2:bool) : bool :=
  match b1 with
  | true ⇒ b2
  | false ⇒ false
  end.
```

```
Definition orb (b1:bool) (b2:bool) : bool :=
  match b1 with
  | true ⇒ true
  | false ⇒ b2
  end.
```

以下四个单元测试演示了多参数应用的语法

```
Example test_orb1: (orb true false) = true.
Proof. simpl. reflexivity. Qed.
Example test_orb2: (orb false false) = false.
Proof. simpl. reflexivity. Qed.
Example test_orb3: (orb false true) = true.
Proof. simpl. reflexivity. Qed.
Example test_orb4: (orb true true) = true.
Proof. simpl. reflexivity. Qed
```

Notation 能为既有的定义赋予新的中缀记法

```
Notation "x && y" := (andb x y).
Notation "x || y" := (orb x y).
Example test_orb5: false || false || true = true.
Proof. simpl. reflexivity. Qed.
```

### **类型**

Check 指令会让 Coq 显示一个表达式的类型

```
Check true.
(* ===> true : bool *)
```

像 negb 这样的函数本身也有类型，被称为函数类型，用带箭头的类型表示

```
Check negb
    : bool → bool.
Check andb
    : bool → bool → bool.
```

### **由旧类型构造新类型**

我们之前定义的枚举类型，每个元素都只是无参数构造子

下面的类型定义，会让其中一个构造子接受一个参数

```
Inductive rgb : Type :=
  | red
  | green
  | blue.
Inductive color : Type :=
  | black
  | white
  | primary (p : rgb).
```

最后一行表示若 p 是属于 rgb 的构造子表达式，则 primary p（构造子 primary 应用于参数 p）是属于集合 color 的构造子表达式

定义一个关于color的函数

```
Definition monochrome (c : color) : bool :=
  match c with
  | black ⇒ true
  | white ⇒ true
  | primary p ⇒ false
  end.
```

```
Definition isred (c : color) : bool :=
  match c with
  | black ⇒ false
  | white ⇒ false
  | primary red ⇒ true
  | primary _ ⇒ false
  end.
```

primary _ 是构造子 primary 应用到除 red 之外的任何 rgb 构造子上

### **元组**

定义一个由四位字节组成的元组

```
Inductive bit : Type :=
  | B0
  | B1.

Inductive nybble : Type :=
  | bits (b0 b1 b2 b3 : bit).

Check (bits B1 B0 B1 B0)
    : nybble.
```

```
Definition all_zero (nb : nybble) : bool :=
  match nb with
    | (bits B0 B0 B0 B0) ⇒ true
    | (bits _ _ _ _) ⇒ false
  end.
```

### **数值**

我们把这个部分放在一个模块中，这样我们自己对自然数的定义就不会干扰标准库中的自然数

```
Module NatPlayground.
```

大写字母O表示零，当S构造函数应用于自然数n的表示时，结果是n+1，其中S代表后继（successor），可被放在一个自然数之前产生另一个自然数

```
Inductive nat : Type :=
  | O
  | S (n : nat).
```

0 → O，1 → S O，2 → S(S O)，3 → S(S(S O))，以此类推

定义自然数的前趋函数

```
Definition pred (n : nat) : nat :=
  match n with
    | O ⇒ O
    | S n' ⇒ n'
  end.
```

定义自然数减法函数

```
Definition minustwo (n : nat) : nat :=
  match n with
    | O ⇒ O
    | S O ⇒ O
    | S (S n') ⇒ n'
  end.
Compute (minustwo 4).
(* ===> 2 : nat *)
```

```
End NatPlayground.
```

Coq 会默认将自然数打印为十进制形式

```
Check (S (S (S (S O)))).
(* ===> 4 : nat *)
```

### **递归**

关键字 Fixpoint 可用于定义递归函数

比如判断自然数是否为偶数

```
Fixpoint evenb (n:nat) : bool :=
  match n with
  | O ⇒ true
  | S O ⇒ false
  | S (S n') ⇒ evenb n'
  end.
```

判断自然数是否为奇数

```
Definition oddb (n:nat) : bool :=
  negb (evenb n).
```

```
Example test_oddb1: oddb 1 = true.
Proof. simpl. reflexivity. Qed.
Example test_oddb2: oddb 4 = false.
Proof. simpl. reflexivity. Qed.
```

递归多参数函数

```
Module NatPlayground2.

Fixpoint plus (n : nat) (m : nat) : nat :=
  match n with
    | O ⇒ m
    | S n' ⇒ S (plus n' m)
  end
```

两个自然数的乘法

```
Fixpoint mult (n m : nat) : nat :=
  match n with
    | O ⇒ O
    | S n' ⇒ plus m (mult n' m)
  end.
Example test_mult1: (mult 3 3) = 9.
Proof. simpl. reflexivity. Qed.
```

两个自然数相减

```
Fixpoint minus (n m:nat) : nat :=
  match n, m with
  | O , _ ⇒ O
  | S _ , O ⇒ n
  | S n', S m' ⇒ minus n' m'
  end.

End NatPlayground2.
```

自然数的幂

```
Fixpoint exp (base power : nat) : nat :=
  match power with
    | O ⇒ S O
    | S p ⇒ mult base (exp base p)
  end.
```

比较两个自然数是否相等

```
Fixpoint eqb (n m : nat) : bool :=
  match n with
  | O ⇒ match m with
         | O ⇒ true
         | S m' ⇒ false
         end
  | S n' ⇒ match m with
            | O ⇒ false
            | S m' ⇒ eqb n' m'
            end
  end.
```

第一个参数是否小于等于第二个参数

```
Fixpoint leb (n m : nat) : bool :=
  match n with
  | O ⇒ true
  | S n' ⇒
      match m with
      | O ⇒ false
      | S m' ⇒ leb n' m'
      end
  end.
```

第一个参数是否严格小于第二个参数

```
Definition ltb (n m:nat) : bool :=
  (negb(eqb n m)) && (leb n m)
```

为了方便我们引入notation来记这几个常用的函数

```
Notation "x + y" := (plus x y)
                       (at level 50, left associativity)
                       : nat_scope.
Notation "x - y" := (minus x y)
                       (at level 50, left associativity)
                       : nat_scope.
Notation "x * y" := (mult x y)
                       (at level 40, left associativity)
                       : nat_scope.
Notation "x =? y" := (eqb x y) (at level 70) : nat_scope.
Notation "x <=? y" := (leb x y) (at level 70) : nat_scope.
```

## **1.2 基于化简的证明**

**simpl** 化简等式两边

**reflexivity** 检查两边是否具有相同的值，会自动做一些化简

**intros** n 假设存在一个任意自然数 n，将量词从证明目标转移到当前假设的上下文中

**Example** 和 **Theorem** 表示完全一样的东西

**策略**是一条可以用在 Proof 和 Qed（证毕）之间的指令，告诉 Coq 如何来检验我们所下的断言的正确性

例如：

```
Theorem plus_O_n : forall n : nat, 0 + n = n.
Proof.
  intros n. reflexivity.  Qed.
```

```
Theorem plus_1_l : forall n:nat, 1 + n = S n.
Proof.
  intros n. reflexivity. Qed.
```

```
Theorem mult_0_l : forall n:nat, 0 * n = 0.
Proof.
  intros n. reflexivity. Qed.
```

后缀 _l 读作“在左边”

simpl的作用总结：

```
1.  Sn' + 0 化为 S (n' + 0)
    Sn' + m 化为 S (n' + m)
    Sn' + Sm 化为 S (n' + S m)
2.  对条件进行化简，simpl可以把S n变成n
3.  去零去括号 0 + (m + p) = 0 + m + p 化为 m + p = m + p
4.  把自己定义的函数转化为自然语言
    double (S n') 化为 S (S (double n'))
```

## **1.3 基于改写的证明**

**intros** 将前提从证明目标移到当前上下文的假设中

**rewrite** 用来告诉 Coq 执行这种替换的策略

**Admitted** 指令告诉 Coq 我们想要跳过此定理的证明

**例子一：**

```
Theorem plus_id_example : ∀ n m:nat,
  n = m →
  n + n = m + m.
```

该定理并未对自然数 n 和 m 所有可能的值做全称断言，而是讨论了仅当 n = m 时这一更加特定情况

```
Proof.
  (* 将两个量词移到上下文中： *)
  intros n m.
  (* 将前提移到上下文中,并将其命名为 H *)
  intros H.
  (* 告诉 Coq 改写当前目标,把前提等式 H 的左边替换成右边 *)
  rewrite → H.
  reflexivity. Qed.
```

→表示把左边替换成右边，←表示把右边替换成左边

便于理解，放个例子

引入前提 H : n = m

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220155255.png)

如果是 -> ，代表把式子里面的n都换成m

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220155355.png)

如果是 <-，表示把式子里的m都换成n，逆向替换

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220160448.png)

**例子二：**

```
Theorem plus_id_exercise : forall n m o : nat,
  n = m -> m = o -> n + m = m + o.
Proof.
  intros n m o H H1.
  rewrite -> H.
  rewrite -> H1.
  reflexivity.
Qed.
```

为了便于理解，具体过程如下

引入前提

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220160551.png)

根据前提 H1：n = m

把式子中的n换成m

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220160642.png)

根据前提 H1：n = m

把式子中的m都换成o

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220160734.png)

**Check** 命令

可用来检查以前声明的引理和定理

```
Check mult_n_O.
(* ===> forall n : nat, 0 = n * 0  *)
Check mult_n_Sm.
(* ===> forall n m : nat, n * m + n = n * S m  *)
```

除了上下文中现有的假设外，还可以通过 rewrite 策略来运用前期证明过的定理

**例子三**

```
Theorem mult_n_0_m_0 : ∀ n m : nat,
  (n × 0) + (m × 0) = 0.
Proof.
  intros n m.
  rewrite <- mult_n_O.
  rewrite <- mult_n_O.
  reflexivity. Qed.
```

**例子四**

```
Theorem mult_n_1 : ∀ n : nat,
  n × 1 = n.
Proof.
  intros.
  rewrite <- mult_n_Sm.
  rewrite <- mult_n_O.
  reflexivity. Qed.
```

**例子五**

```
Theorem mult_0_plus : forall n m : nat,
  (0 + n) * m = n * m.
Proof.
  intros n m.
  rewrite -> plus_O_n.
  reflexivity.  Qed.
```

**例子六**

```
Theorem mult_S_1 : forall n m : nat,
  m = S n ->
  m * (1 + n) = m * m.
Proof.
  intros n m H.
  simpl.
  rewrite <- H.
  reflexivity.
Qed.
```

## **1.4 基于情况分析的证明**

**destruct** 分别对 n = 0 和 n = S n' 这两种情况进行分析的策略

**例一**

```
Theorem plus_1_neq_0 : forall n : nat,
  beq_nat (n + 1) 0 = false.
Proof.
  intros n. destruct n as [| n'].
  - reflexivity.
  - reflexivity.
Qed.
```

**destruct** 生成两个子目标，然后我们分别证明

**as [| n']** 是介绍模式，指出变量，变量之间用|分开。第一个组件是空的，因为O的构造函数是空的，第二个组件n'，因为S是一元构造函数

**eqn:E** 注释告诉析构函数给这个方程命名E

**— 符号** 标明这两个生成的子目标所对应的证明部分

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220164856.png)

**例二**

证明布尔值的取反是对合（Involutive）的

```
Theorem negb_involutive : forall b : bool,
  negb (negb b) = b.
Proof.
  intros b. destruct b.
  - reflexivity.
  - reflexivity.  Qed.
```

destruct 没有 as 子句，因为此处 destruct 生成的子分类均无需绑定任何变量

b分成了true和false两种情况讨论

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220165232.png)

**例三**

在一个子目标内调用 destruct，产生出更多的证明义务，使用不同的标号来标记目标的不同层级

```
Theorem andb_commutative : ∀ b c, andb b c = andb c b.
Proof.
  intros b c. destruct b
  - destruct c eqn:Ec.
    + reflexivity.
    + reflexivity.
  - destruct c eqn:Ec.
    + reflexivity.
    + reflexivity.
Qed.
```

具体过程如下：

引入变量b c

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220165450.png)

分别讨论b为true和b为false两种情况

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220165535.png)

在b为true的情况下，分别讨论c为true和c为false两种情况

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220165619.png)

除了 - 和 + 之外，还可以使用 ×  -- ***，也可以用花括号将每个子证明目标括起来

```
Theorem andb_commutative' : ∀ b c, andb b c = andb c b.
Proof.
  intros b c. destruct b
  { destruct c
    { reflexivity. }
    { reflexivity. } }
  { destruct c
    { reflexivity. }
    { reflexivity. } }
Qed.
```

花括号还允许我们在一个证明中的多个层级下使用同一个标号

```
Theorem andb3_exchange :
  ∀ b c d, andb (andb b c) d = andb (andb b d) c.
Proof.
  intros b c d. destruct b eqn:Eb.
  - destruct c eqn:Ec.
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
  - destruct c eqn:Ec.
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
Qed.
```

最后说一种简便写法，很多证明在引入变量之后会立即对它进行情况分析：

```
intros x y. destruct y as [|y] eqn:E.
```

但可以通过使用介绍模式而不是变量名来对变量进行案例分析

```
Theorem plus_1_neq_0' : ∀ n : nat,
  (n + 1) =? 0 = false.
Proof.
  intros [|n].
  - reflexivity.
  - reflexivity. Qed.
```

如果没有需要命名的构造子参数，只需写上 [] 即可进行情况分析

```
Theorem andb_commutative'' :
  forall b c, andb b c = andb c b.
Proof.
  intros [] [].
  - reflexivity.
  - reflexivity.
  - reflexivity.
  - reflexivity.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220171813.png)

**练习一**

```
Theorem zero_nbeq_plus_1 : forall n : nat,
  0 =? (n + 1) = false.
Proof.
  intros [| n'].
  -simpl. reflexivity.
  -simpl. reflexivity.
Qed.
```

熟练使用简化的引入写法

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220172406.png)

**练习二**

```
Theorem andb_true_elim2 : forall b c : bool,
  andb b c = true -> c = true.
Proof.
  intros [] [].
  - reflexivity.
  - intro H.
    rewrite <- H.
    reflexivity.
  - reflexivity.
  - intro H.
    rewrite <- H.
    reflexivity.
Qed.
```

说明一下第二种情况和第四种情况的过程，之前一直无法理解

引入 false && false  = true 的条件，想要证明的结论是 false = true

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220172152.png)

把 条件中的true rewrite 为 false && false

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211220172213.png)

## **1.5 递归函数Fixpoint**

## **1.6 更多练习**

**练习一**

证明以下关于布尔函数的定理

```
Theorem identity_fn_applied_twice :
  forall (f : bool -> bool),
  (forall (x : bool), f x = x) ->
  forall (b : bool), f (f b) = b.
Proof.
  intros f H b.
  rewrite -> H.
  rewrite -> H.
  reflexivity.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221005427.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221005441.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221005455.png)

**练习二**

```
Theorem negation_fn_applied_twice :
  forall (f : bool -> bool),
  (forall (x : bool), f x = negb x) ->
  forall (b : bool), f (f b) = b.
Proof.
  intros f H b.
  rewrite -> H.
  rewrite -> H.
  rewrite -> negb_involutive.
  reflexivity.
Qed.

其中
negb_involutive
     : forall b : bool, negb (negb b) = b
```

**练习三**

```
Theorem andb_eq_orb :
  forall (b c : bool),
  (andb b c = orb b c) ->
  b = c.
Proof.
  intros b c H.
  destruct b.
  - destruct c.
    + reflexivity.
    + simpl in H.
      rewrite -> H. reflexivity.
  - destruct c.
    + simpl in H.
      rewrite -> H. reflexivity.
    + reflexivity.
Qed.
```

# **二、INDUCTION**

## **2.1 归纳证明**

在开始之前把上一章所有的定义都导入进来

在 CoqIDE 中：Open Basics.v，complie → compile buffer → make makefile

然后 Open Induction.v

```
From LF Require Export Basics.
```

证明这种关于数字、列表等归纳定义的集合， 我们通常需要一个更强大的推理原理：归纳

方法：通过应用 induction，把它分为两个子目标：

- 一个是我们必须证明 P(O) 成立
- 另一个是我们必须证明 P(n') → P(S n')

### **例题**

**例子一：**

```
Theorem plus_n_O : forall n:nat, n = n + 0.
Proof.
  intros n. induction n as [| n' IHn'].
  - (* n = 0 *)    reflexivity.
  - (* n = S n' *) simpl. rewrite <- IHn'. reflexivity.  Qed.
```

具体过程如下：

通过induction as分成两种情况，用|隔开

在第一个子目标中n被0取代

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221192156.png)

在第二个目标中，n 被 S n' 取代，IHn' ：n’ = n' + 0 是已知前提

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221192215.png)

待证目标变成了 (S n') + 0 = S n'，它可被simpl化简为 S (n' + 0) = S n'，而此结论可通过 IHn' 得出

这里没太懂

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221192230.png)

改写

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221192246.png)

**例子二**

```
Theorem minus_diag : forall n,
  minus n n = 0.
Proof.
  intros n. induction n as [| n' IHn'].      // IHn' : n' - n' = 0
  - (* n = 0 *)
    simpl. reflexivity.
  - (* n = S n' *)            // S n' - S n' = 0
    simpl.                    // n' - n' = 0
    rewrite -> IHn'.          // 0 = 0
    reflexivity.  Qed.
```

这里没懂

好像知道了simpl的作用，可以把 S n' 化成 n'，不知道为啥

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221193013.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221193024.png)

### **练习**

**练习一**

```
Theorem mult_0_r : forall n:nat,
  n * 0 = 0.
Proof.
  intros n.
  induction n as [|n' IHn].
  - reflexivity.
  - simpl. rewrite -> IHn. reflexivity. Qed.
```

好像知道了simpl的作用，可以把 S n' 化成 n'，不知道为啥

```
Theorem plus_n_Sm : forall n m : nat,
  S (n + m) = n + (S m).
Proof.
  intros n m.
  induction n as [|n' IHn].
  - reflexivity.
  - simpl. rewrite -> IHn. reflexivity.
Qed.
```

好像知道了simpl的另一个作用，可以把 S n' + m 化成 S (n' + m)

```
Theorem plus_comm : forall n m : nat,
  n + m = m + n.
Proof.
  intros n m.
  induction n as [|n' IHn].   //  IHn : n' + m = m + n'
  - (* n = 0 *)
    simpl.
    rewrite <- plus_n_O.
    reflexivity.
  - (* n = S n' *)             //  S n' + m = m + S n'
    simpl.                     //  S (n' + m) = m + S n'
    rewrite -> IHn.            //  S (m + n') = m + S n'
    rewrite -> plus_n_Sm.      //  m + S n' = m + S n'
    reflexivity.
Qed.

其中
plus_n_O
     : forall n : nat, n = n + 0

plus_n_Sm
     : forall n m : nat, S (n + m) = n + S m
```

```
Theorem plus_assoc : forall n m p : nat,
  n + (m + p) = (n + m) + p.
Proof.
  intros n m p.
  induction n as [|n' IHn].                 // IHn : n' + (m + p) = n' + m + p
  - reflexivity.
  - (* n = S n' *)             //  S n' + (m + p) = S n' + m + p
    simpl.                     //  S (n' + (m + p)) = S (n' + m + p)
    rewrite -> IHn.            //  S (n' + m + p) = S (n' + m + p)
    reflexivity.
Qed.
```

**练习二**

前提

```
Fixpoint double (n:nat) :=
  match n with
  | O => O
  | S n' => S (S (double n'))
  end.
```

用归纳法证明

```
Lemma double_plus : forall n, double n = n + n .
Proof.
  intros n.
  induction n as [|n' IHn].      // double n' = n' + n'
  - (* n = 0 *)
    reflexivity.
  - (* n = S n' *)               // double (S n') = S n' + S n'
   simpl.                        // S (S (double n')) = S (n' + S n')
   rewrite -> IHn.               // S (S (n' + n')) = S (n' + S n')
   rewrite <- plus_n_Sm.         // S (S (n' + n')) = S (S (n' + n'))
   reflexivity.
Qed.

其中

plus_n_Sm
     : forall n m : nat, S (n + m) = n + S m
```

**练习三**

```
Check negb_involutive.
Theorem evenb_S : forall n : nat,
  evenb (S n) = negb (evenb n).
Proof.
  intros n.
  induction n as [|n' IHn].            //  IHn : evenb (S n') = negb (evenb n')
  - reflexivity.
  -                                    //  evenb (S (S n')) = negb (evenb (S n'))
    rewrite -> IHn.                    //  evenb (S (S n')) = negb (negb (evenb n'))
    rewrite -> negb_involutive.        //  evenb (S (S n')) = evenb n'
    reflexivity.
Qed.

其中
negb_involutive
     : forall b : bool, negb (negb b) = b
```

### **辨析**

一直没懂什么时候用基于化简，什么时候用基于归纳

0在n左边的时候用化简，0在n右边的时候用归纳

0 + n = n ，n = 0 + n 用化简，n + 0 = n，n = n + 0用归纳

0 * n = 0 用化简，n * 0 = 0用归纳

因为 0 * n = 0 可以被simpl. 后者不行

前者 simpl 结果

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221193907.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221193918.png)

后者 simpl 结果，没有变化，这只能用归纳了

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221194002.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211221194013.png)

## **2.2 证明里的证明**

在 Coq 中，大的证明通常会被分为一系列定理， 后面的定理引用之前的定理

例如，我们之前对 mult_0_plus 定理的证明引用了前一个名为 plus_O_n 的定理

```
Theorem mult_0_plus : forall n m : nat,
  (0 + n) * m = n * m.
Proof.
  intros n m.
  rewrite -> plus_O_n.
  reflexivity.  Qed.
```

而我们只需使用 assert 就能陈述并证明 plus_O_n，后面的大括号内容是证明过程

```
Theorem mult_0_plus' : forall n m : nat,
  (0 + n) * m = n * m.
Proof.
  intros n m.
  assert (H: 0 + n = n). { reflexivity. }
  rewrite -> H.
  reflexivity.  Qed.
```

另一个例子

为了在需要的地方使用我们的小定理，可以引入一个局部引理来陈述 n + m = m + n，之后用 plus_comm 证明它， 并用它来进行期望的改写

```
Theorem plus_rearrange : forall n m p q : nat,
  (n + m) + (p + q) = (m + n) + (p + q).
Proof.
  intros n m p q.
  assert (H: n + m = m + n).
  { rewrite -> plus_comm. reflexivity. }
  rewrite -> H. reflexivity.  Qed.
```

## **2.3 形式化证明**

形式化证明和非形式化证明的对比

非形式化证明是算法，形式化证明是代码

一方面，“读者”可以是像 Coq 这样的程序， 此时灌输的是 P 能够从一个确定的，由形式化逻辑规则组成的集合中机械地推导出来，而证明则是指导程序检验这一事实的方法。这种方法就是形式化证明

另一方面，读者也可以是人类，这种情况下证明可以用英语或其它自然语言写出， 因此必然是非形式化的

由于我们在本课程中使用 Coq，因此会重度使用**形式化证明**

但这并不意味着我们 可以完全忽略掉非形式化的证明过程！

## **2.4 更多练习**

**练习一**

可以不用归纳

```
Theorem plus_swap : forall n m p : nat,
  n + (m + p) = m + (n + p).
Proof.
  intros n m p.                            //  n + (m + p) = m + (n + p)
  rewrite -> plus_assoc.                   //  n + m + p = m + (n + p)
  assert (H: n + m = m + n).
  { rewrite -> plus_comm.  reflexivity. }
  rewrite -> H.                            //  n + m + p = n + (m + p)
  rewrite -> plus_assoc.                   //  n + m + p = n + m + p
  reflexivity.
Qed.

plus_assoc
     : forall n m p : nat, n + (m + p) = n + m + p

plus_comm
     : forall n m : nat, n + m = m + n
```

复习一下如果用归纳做，好像不是同一道题

```
Theorem plus_assoc : forall n m p : nat,
  n + (m + p) = (n + m) + p.
Proof.
  intros n m p.
  induction n as [|n' IHn].                 // IHn : n' + (m + p) = n' + m + p
  - reflexivity.
  - (* n = S n' *)             //  S n' + (m + p) = S n' + m + p
    simpl.                     //  S (n' + (m + p)) = S (n' + m + p)
    rewrite -> IHn.            //  S (n' + m + p) = S (n' + m + p)
    reflexivity.
Qed.
```

**练习二**

```
Theorem mult_n_Sm: forall n m : nat,
  n * S m = n + n * m.
Proof.
  intros n m.
  induction n as [|n' IHn].           //  IHn : n' * S m = n' + n' * m
  - (* n = 0 *)
    reflexivity.
  - (* n = S n' *)                    //  S n' * S m = S n' + S n' * m
    simpl.                            //  S (m + (n' + n' * m)) = S (n' + (m + n' * m))
    rewrite -> IHn.                   //  S (n' + (m + n' * m)) = S (n' + (m + n' * m))
    rewrite plus_swap.
    reflexivity.
Qed.
```

**练习三**

```
Theorem mult_comm : forall m n : nat,
  m * n = n * m.
Proof.
  intros n m.
  induction n as [|n' IHn].
  - rewrite -> mult_0_l.
    rewrite <- mult_n_O.
    reflexivity.
  - simpl.
    rewrite -> IHn.
    rewrite -> mult_n_Sm.
    reflexivity.
Qed.
```

**练习四**

区分什么时候该用什么方法

(a) 它能否能只用化简和改写来证明

(b) 它还需要分类讨论（destruct）

(c) 它还需要归纳证明

```
Theorem leb_refl : forall n:nat,
  true = leb n n.
Proof.
  intros n.
  induction n as [|n' IHn].
  - (* n = 0 *)
    reflexivity.
  - simpl. rewrite <- IHn. reflexivity.
Qed.
```

```
Theorem zero_nbeq_S : forall n:nat,
  beq_nat 0 (S n) = false.
Proof.
  intros n.
  simpl.
  reflexivity.
Qed.
```

```
Theorem S_nbeq_0 : forall n:nat,
  beq_nat (S n) 0 = false.
Proof.
  reflexivity.
Qed.

```

```
Theorem plus_ble_compat_l : forall n m p : nat,
  leb n m = true -> leb (p + n) (p + m) = true.
Proof.
  intros n m p H.
  induction p as [|p' IHp].
  - simpl.
    rewrite -> H.
    reflexivity.
  - simpl.
    rewrite -> IHp.
    reflexivity.
Qed.
```

```
Theorem mult_1_l : forall n:nat, 1 * n = n.
Proof.
  intros n.
  simpl. rewrite <- plus_n_O. reflexivity.
Qed.
```

这里simpl又可以把 1 * n = n 改写为 n + 0 = n，真是搞不懂

```
Theorem mult_plus_distr_r : forall n m p : nat,
  (n + m) * p = (n * p) + (m * p).
Proof.
  intros n m p.
  induction n as [|n' IHn].
  - reflexivity.
  - simpl.
    rewrite -> IHn.
    rewrite -> plus_assoc.
    reflexivity.
Qed.
```

## **2.5 本章可以复用的定理总结**

```
 plus_n_O : n = n + 0.
 plus_n_Sm : S (n + m) = n + (S m).
 plus_comm : n + m = m + n.
 plus_swap : n + (m + p) = m + (n + p).
 plus_assoc : n + (m + p) = (n + m) + p.

 mult_n_O : 0 = n * 0.
 mult_n_Sm: n * S m = n + n * m.
 mult_comm : m * n = n * m.
 mult_0_l : 0 * n = 0.
 mult_0_r : n * 0 = 0.
 mult_assoc : n * (m * p) = n * m * p

 negb_involutive : negb (negb b) = b
```

# **三、LIST**

## **3.1 数值序对**

定义pair 数值序对

```
Inductive natprod : Type :=
| pair (n1 n2 : nat).
```

提取pair的第一个和第二个元素

```
Definition fst (p : natprod) : nat :=
  match p with
  | pair x y => x
  end.

Definition snd (p : natprod) : nat :=
  match p with
  | pair x y => y
  end.
```

用notion简化一下表示

```
Notation "( x , y )" := (pair x y).

//notion的符号也可以应用于 pattern match

Definition fst' (p : natprod) : nat :=
  match p with
  | (x,y) => x
  end.

Definition snd' (p : natprod) : nat :=
  match p with
  | (x,y) => y
  end.

Definition swap_pair (p : natprod) : natprod :=
  match p with
  | (x,y) => (y,x)
  end.
```

**下面证明一些二元组性质**

可以直接证明

```
Theorem surjective_pairing' : forall (n m : nat),
  (n,m) = (fst (n,m), snd (n,m)).
Proof.
  reflexivity.  Qed.
```

p的结构不明显时，用destruct

```
Theorem surjective_pairing : forall (p : natprod),
  p = (fst p, snd p).
Proof.
  intros p.
  destruct p as [n m].         // (n,m) = (fst (n,m), snd (n,m))
  reflexivity.  Qed.
```

练习 1星

猜想simpl应该是根据前面定义过的 defination来化简得？

```
Theorem snd_fst_is_swap : forall (p : natprod),
  (snd p, fst p) = swap_pair p.
Proof.
  intros p.
  destruct p as [n m].          //  (snd (n, m), fst (n, m)) = swap_pair (n, m)
  simpl.                        //  (m, n) = (m, n)
  reflexivity.
Qed.
```

练习 1星

```
Theorem fst_swap_is_snd : forall (p : natprod),
  fst (swap_pair p) = snd p.
Proof.
  intros p.
  destruct p as [n m].
  simpl.
  reflexivity.
Qed.
```

## **3.2 数值列表**

一个列表要么是空的，要么就是由一个数和另一个列表组成的序对

```
Inductive natlist : Type :=
  | nil  : natlist
  | cons (n : nat) (1 : natlist).
```

如下是一个三元素的列表

```
Definition mylist := cons 1 (cons 2 (cons 3 nil)).
```

声明一些符号简化一下

注意 + 号比 :: 结合符号优先级更高，会先结合

```
Notation "x :: l" := (cons x l)
                     (at level 60, right associativity).
Notation "[ ]" := nil.
Notation "[ x ; .. ; y ]" := (cons x .. (cons y nil) ..).
Notation "x ++ y" := (app x y)
                     (right associativity, at level 60).
```

**接下来是一些构造和操作列表的函数**

返回一个长度为 count，每个元素都是 n 的列表

```
Fixpoint repeat (n count : nat) : natlist :=
  match count with
  | O => nil
  | S count' => n :: (repeat n count')
  end.
```

计算列表的长度

```
Fixpoint length (l:natlist) : nat :=
  match l with
  | nil => O
  | n :: t => S (length t)
  end.
```

把两个列表联接起来

```
Fixpoint app (l1 l2 : natlist) : natlist :=
  match l1 with
  | nil   => l2
  | h :: t => h :: (app t l2)
  end.
```

返回列表第一个元素

由于空表没有表头，所以传入了default

```
Definition hd (default:nat) (l:natlist) : nat :=
  match l with
  | nil => default
  | h :: t => h
  end.
```

返回列表除去第一个元素以外的部分

```
Definition tl (l:natlist) : natlist :=
  match l with
  | nil => nil
  | h :: t => t
  end.
```

**下面进行一些列表练习**

去除列表里的0

```
Fixpoint nonzeros (l:natlist) : natlist :=
  match l with
  | nil => []
  | 0 :: t => nonzeros t
  | h :: t => h :: (nonzeros t)
  end.
```

返回列表中的奇数

if then else 的形式不用打箭头

```
Fixpoint oddmembers (l:natlist) : natlist :=
  match l with
  | nil => []
  | h :: t =>
      if oddb h then h :: (oddmembers t)
      else oddmembers t
  end.
```

从两个列表中交替地取出元素并合并为一个列表

```
Fixpoint alternate (l1 l2 : natlist) : natlist :=
  match l1 with
  | nil => l2
  | h1 :: t1 => match l2 with
            | nil => l1
            | h2 :: t2 => h1 :: h2 :: (alternate t1 t2)
            end
  end.
```

## **3.3 口袋**

bag（或者叫 multiset 多重集）类似于集合，只是其中每个元素都能出现不止一次

口袋的一种可行的表示是列表

```
Definition bag := natlist.
```

**下面为口袋设定一些函数**

计算出现此处

```
Fixpoint count (v:nat) (s:bag) : nat :=
  match s with
  | [] => O
  | h :: t =>
      if beq_nat v h then S (count v t)
      else count v t
  end.
```

append

```
Definition sum : bag -> bag -> bag := app.
```

number append list

```
Definition add : nat -> bag -> bag := cons.
```

member

```
Definition member (v:nat) (s:bag) : bool :=
  if beq_nat O (count v s) then false
  else true.
```

去除一个跟v相同的列表元素

```
Fixpoint remove_one (v:nat) (s:bag) : bag :=
  match s with
  | nil => nil
  | h :: t =>
              if beq_nat v h then t
              else h :: remove_one v t
  end.
```

去除所有跟v相同的列表元素

```
Fixpoint remove_all (v:nat) (s:bag) : bag :=
  match s with
  | [] => []
  | h :: t =>
      if beq_nat v h then (remove_all v t)
      else h :: (remove_all v t)
  end.
```

判断子集

逻辑是一旦遇到s1中有不在s2中的元素就 return false

记得判断之后要remove_one！

```
Fixpoint subset (s1:bag) (s2:bag) : bool :=
  match s1 with
  | [] => true
  | h :: t =>
      if beq_nat O (count h s2) then false
      else subset t (remove_one h s2)
  end.

Example test_subset2:              subset [1;2;2] [2;1;4;1] = false.
Proof. simpl. reflexivity. Qed.
```

## **3.4 有关列表的论证**

**基于化简的证明**

```
Theorem nil_app : forall l:natlist,
  [] ++ l = l.
Proof. reflexivity. Qed.
```

**基于分情况的证明**

```
Theorem tl_length_pred : forall l:natlist,
  pred (length l) = length (tl l).
Proof.
  intros l. destruct l as [| n l'].
  - reflexivity.
  - reflexivity.  Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211222170521.png)

**列表的归纳证明**

列表可以用 nil 或者将 cons 应用到一个自然数和另一个列表上来构造

一个列表要么是 nil， 要么就是 cons 应用到某个数字和某个更小的列表上

- 首先，证明当 l 为 nil 时，p l 成立
- 然后，证明当 l 为 cons n l' 时 P l 成立，其中 n 是某个自然数，l' 是某个更小的列表，假设 P l' 成立

**例子：**

```
Theorem app_assoc : forall l1 l2 l3 : natlist,
  (l1 ++ l2) ++ l3 = l1 ++ (l2 ++ l3).
Proof.
  intros l1 l2 l3. induction l1 as [| n l1' IHl1'].  // IHl1' : (l1' ++ l2) ++ l3 = l1' ++ l2 ++ l3
  - (* l1 = nil *)
    reflexivity.
  - (* l1 = cons n l1' *)                   //  ((n :: l1') ++ l2) ++ l3 = (n :: l1') ++ l2 ++ l3
    simpl.                                  //  n :: (l1' ++ l2) ++ l3 = n :: l1' ++ l2 ++ l3
    rewrite -> IHl1'.                       //  n :: l1' ++ l2 ++ l3 = n :: l1' ++ l2 ++ l3
    reflexivity.  Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211222171052.png)

**反转列表：**

# **四、POLY**

# **五、TACITCS**

## **5.1 Apply**

```
Theorem silly1 : forall (n m o p : nat),
     n = m  ->
     [n;o] = [n;p] ->
     [n;o] = [m;p].
Proof.
  intros n m o p eq1 eq2.
  rewrite <- eq1.
  apply eq2.  Qed.
```

当我们在以下证明中执行 apply eq2 时，eq2 中的通用变量 q 会以 n 实例化，而 r 会以 m 实例化

```
Theorem silly2 : forall (n m o p : nat),
     n = m  ->
     (forall (q r : nat), q = r -> [q;o] = [r;p]) ->
     [n;o] = [m;p].
Proof.
  intros n m o p eq1 eq2.
  apply eq2. apply eq1.  Qed.
```

```
Theorem silly2a : forall (n m : nat),
     (n,n) = (m,m)  ->
     (forall (q r : nat), (q,q) = (r,r) -> [q] = [r]) ->
     [n] = [m].
Proof.
  intros n m eq1 eq2.
  apply eq2. apply eq1.  Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226125641.png)

下面这里没懂为什么是apply h0

```
Theorem silly_ex :
     (forall n, evenb n = true -> oddb (S n) = true) ->
     oddb 3 = true ->
     evenb 4 = true.
Proof.
  intros H H0.
  apply H0.
Qed.
```

当等式的左右两边互换后，apply 就无法起效了

我们无法直接使用 apply，不过我们可以用 **symmetry 策略**，它会交换证明目标中等式的左右两边

```
Theorem silly3_firsttry : forall (n : nat),
     true = beq_nat n 5  ->
     beq_nat (S (S n)) 7 = true.
Proof.
  intros n H.
  symmetry.
  simpl.
  apply H.  Qed.
```

**Apply with**

等式的传递性！**想要证明等式的传递性，但等式两边并非自然数，就用trans_eq这个定理！**

比如我们可以把以下自然数等式的传递性，推广到数列的传递性

```
Theorem trans_eq : forall (X:Type) (n m o : X),
  n = m -> m = o -> n = o.
Proof.
  intros X n m o eq1 eq2. rewrite -> eq1. rewrite -> eq2.
  reflexivity.  Qed.
```

只需传递一个数列参数，apply with 的参数是想要把结论的右式替换为的那个，比如这里是想把结论里的[e:f]替换为[c:d]

```
Example trans_eq_example' : forall (a b c d e f : nat),
     [a;b] = [c;d] ->
     [c;d] = [e;f] ->
     [a;b] = [e;f].
Proof.
  intros a b c d e f eq1 eq2.
  apply trans_eq with [c;d].
  apply eq1. apply eq2.   Qed.
```

一个分别apply的过程

```
Example trans_eq_exercise : forall (n m o p : nat),
     m = (minustwo o) ->
     (n + p) = m ->
     (n + p) = (minustwo o).
Proof.
  intros n m o p H H0.
  apply trans_eq with m.
  apply H0. apply H.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226131737.png)

## **5.2 Injection**

利用单射性直接从条件中推导出更多的隐含条件，并且apply

关键词：injection inversion

使用 Basics.v 中的 pred 函数来证明 S 的单射性

```
Theorem S_injective : ∀ (n m : nat),
  S n = S m →
  n = m.
Proof.
  intros n m H1.
  assert (H2: n = pred (S n)). { reflexivity. }
  rewrite H2. rewrite H1. reflexivity.
Qed.
```

也可以通过 **inversion H**，我们要求 Coq 生成它可以从 H 推断出的所有方程作为额外的假设，随着它的进行替换目标中的变量。在本示例中，这相当于添加一个新的假设 H1 : n = m 并将目标中的 n 替换为 m

```
Theorem S_injective : forall (n m : nat),
  S n = S m ->
  n = m.
Proof.
  intros n m H.
  inversion H.
  reflexivity.
Qed.
```

**inversion exercise 1**

```
Theorem inversion_ex1 : forall (n m o : nat),
  [n; m] = [o; o] ->
  [n] = [m].
Proof.
  intros n m o H.
  inversion H.
  rewrite <- H1.
  reflexivity. Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226133646.png)

**inversion exercise 2**

inversion H as [Hnm]

```
Theorem inversion_ex2 : forall (n m : nat),
  [n] = [m] ->
  n = m.
Proof.
  intros n m H. inversion H. reflexivity.  Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226133758.png)

**inversion exercise 3**

```
Example inversion_ex3 : forall (X : Type) (x y z w : X) (l j : list X),
  x :: y :: l = w :: z :: j ->
  x :: l = z :: j ->
  x = y.
Proof.
  intros X x y z w l j H H0.
  inversion H.
  inversion H0.
  apply trans_eq with x.
  symmetry.
  apply H2.
  apply H5.
Qed.
```

从 H 可以推出 H2 H3 H4

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226133932.png)

从 H0 可以推出 H5 H6

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226134030.png)

这个apply with没看懂，我带入z y w都不太对

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226134412.png)

单射的逆形式

```
Theorem f_equal : forall (A B : Type) (f: A -> B) (x y: A),
  x = y -> f x = f y.
Proof.
  intros A B f x y eq.
  rewrite eq.
  reflexivity.  Qed.
```

## **5.3 Disjointness**

不相交性

以不同构造函数（如 O 和 S，true，false）开头的两个术语永远不可能相等

**desciminate 策略**用于涉及不同构造函数之间相等的假设（例如，S n = O），它立即解决当前目标

```
Theorem beq_nat_0_l : forall n,
   beq_nat 0 n = true -> n = 0.
Proof.
  intros n.
  destruct n as [| n].
  - (* n = 0 *) reflexivity.
  - (* n = S n' *)
    simpl.
    intros H.
    discriminate H. Qed.
```

对于这道例题，我的理解是，条件是 0\geq n，结论是 n=0，因此我们要做的就是排除掉 n>0 的情况，也就是证明这种情况是错的，先用 destruct 把两种情况分开，证明第一个是对的，第二个是错的

如果我们对这个假设使用 **discriminate** ， Coq 便会确认我们当前正在证明的目标不可行，并同时移除它，不再考虑

另外我发现，injection和descriminate策略都可以用 **inversion** 关键字代替

discriminate exercise 1

下面是**爆炸原理**的一个实例，**矛盾的前提会推出任何东西， 甚至是假命题**！

```
Theorem inversion_ex4 : forall (n : nat),
  S n = O ->
  2 + 2 = 5.
Proof.
  intros n H. discriminate H. Qed.
```

```
Theorem inversion_ex5 : forall (n m : nat),
  false = true ->
  [n] = [m].
Proof.
  intros n m H. discriminate H. Qed.
```

discriminate exercise 2

```
Example inversion_ex6 : forall (X : Type)
                          (x y z : X) (l j : list X),
  x :: y :: l = [] ->
  y :: l = z :: j ->
  x = z.
Proof.
  intros X x y z l j H H0.
  discriminate H.
Qed.
```

## **5.4 对假设使用策略**

默认情况下，大部分策略会作用于目标公式并保持上下文不变。其实也可以对假设进行变体

```
Theorem S_inj : forall (n m : nat) (b : bool),
     beq_nat (S n) (S m) = b  ->
     beq_nat n m = b.
Proof.
  intros n m b H.
  simpl in H.           //对条件进行化简，simpl可以把S n变成n
  rewrite H.
  reflexivity.  Qed.
```

```
Theorem silly3' : forall (n : nat),
  (beq_nat n 5 = true -> beq_nat (S (S n)) 7 = true) ->
  true = beq_nat n 5  ->
  true = beq_nat (S (S n)) 7.
Proof.
  intros n eq H.
  symmetry in H.
  apply eq in H.
  symmetry in H.
  apply H.  Qed.

```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220212111457.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220212111502.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220212111454.png)

## **5.5 对假设进行归纳**

好像是用来证明有两个参数的函数的单射性

先induction再destruct，真是看不懂。。。

**例题一：**

```
Theorem plus_n_n_injective : forall n m,
     n + n = m + m ->
     n = m.
Proof.
  intros n. induction n as [| n'].
  - (* n = O *) intros m H.
    destruct m as [|m'].
    + (* m = O *)  reflexivity.
    + (* m = S m' *) inversion H.
  - (* n = S n' *) intros m H.
    destruct m as [|m'].
    + (* m = O *)  inversion H.
    + (* m = S m' *)
      apply f_equal.
      apply IHn'.
      simpl in H.
      rewrite <- plus_n_Sm in H.
      rewrite <- plus_n_Sm in H.
      inversion H.
      reflexivity.
Qed.
```

1. 这里用inversion是个啥意思，万物都可inversion
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220212201235.png)
    
2. 要S n' = S m' 变成n' = m'，这里还用的不是simpl，而是 f_equal.
3. 从 S (S (n' + n')) = S (S (m' + m')) 得到n' + n' = m' + m'，直接用inversion

**例题二：**

```
Theorem double_injective : forall n m,
     double n = double m ->
     n = m.
Proof.
  intros n. induction n as [| n'].
  - (* n = O *) simpl. intros m eq. destruct m as [| m'].
    + (* m = O *) reflexivity.
    + (* m = S m' *) inversion eq.

  - (* n = S n' *) simpl.
    intros m eq.
    destruct m as [| m'].
    + (* m = O *) simpl.
      inversion eq.
    + (* m = S m' *)
      apply f_equal.
      apply IHn'. simpl in eq. inversion eq. reflexivity. Qed.
```

1. 总的套路是先intros n，induction n，再在每个分类里 intros m H，destruct m
2. apply的作用：已知 条件 → 结果，和证明结果，可以推出条件

**例题三：**

套路是一样的，一定要记住在第四个part的证明里用到IHn！！一定要记住

一眼能看出来的结论用inversion试试

```
Theorem beq_nat_true : forall n m,
    beq_nat n m = true -> n = m.
Proof.
  intro n.
  induction n as [|n' IHn].
  - intros m H. destruct m as [| m'].
    + reflexivity.
    + simpl in H. inversion H.
  - intros m H. destruct m as [| m'].
    + inversion H.
    + apply f_equal.
      inversion H.
      apply IHn.   //一定要记住在第四个part的证明里用到IHn！！一定要记住
      apply H1.
Qed.
```

**例题四：**

看不懂

```
Theorem nth_error_after_last: forall (n : nat) (X : Type) (l : list X),
     length l = n ->
     nth_error l n = None.
Proof.
  intros n X l H.
  generalize dependent n.
  induction l as [|m' l' IHl].
  - (* l = nil *) reflexivity.
  - (* l = m' :: l' *)
    intros n H.
    destruct n as [|n'].
    + (* n = O *) inversion H.
    + (* n = S n' *)
      simpl. inversion H. apply IHl.
      reflexivity.
Qed.
```

## **5.6 Unfold**

有时我们需要手动展开由定义引入的名称，以便我们可以操纵它表示的表达式

```
Lemma square_mult : forall n m, square (n * m) = square n * square m.
Proof.
  intros n m.
  simpl.
  unfold square.           // n * m * (n * m) = n * n * (m * m)
  rewrite mult_assoc.      // n * m * n * m = n * n * (m * m)
  rewrite my_assoc.        // n * n * m * m = n * n * (m * m)
  rewrite mult_assoc.      // n * n * m * m = n * n * m * m
  reflexivity.
Qed.

其中
Theorem my_assoc : forall n m:nat, n * m * n = n * n * m.
Proof.
  intros n m.
  rewrite mult_comm.
  rewrite mult_assoc.
  reflexivity.
Qed.
```

记住一下

mult_assoc  n * (m * p) = n * m * p

mult_comm  m * n = n * m

**下一个例子**

对于用模式匹配定义的常数函数

```
Definition bar x :=
  match x with
  | O => 5
  | S _ => 5
  end.
```

要想证明关于它的函数有两种方法

一种是用destruct分成两种情况，可以发现simpl也可以起到局部unfold的作用

```
Fact silly_fact_2 : forall m, bar m + 1 = bar (m + 1) + 1.
Proof.
  intros m.
  destruct m.
  - simpl. reflexivity.
  - simpl. reflexivity.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220213095911.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220213095924.png)

一种是用unfold展开

```
Fact silly_fact_2' : forall m, bar m + 1 = bar (m + 1) + 1.
Proof.
  intros m.
  unfold bar.
  destruct m.
  - reflexivity.
  - reflexivity.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226155037.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226155113.png)

## **5.7 对复合表达式使用 destruct**

对于if else的情况可以用destruct来分解

```
Definition sillyfun (n : nat) : bool :=
  if beq_nat n 3 then false
  else if beq_nat n 5 then false
  else false.

Theorem sillyfun_false : forall (n : nat),
  sillyfun n = false.
Proof.
  intros n. unfold sillyfun.
  destruct (beq_nat n 3).
    - reflexivity.
    - destruct (beq_nat n 5).
      + reflexivity.
      + reflexivity.  Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226155418.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220213100355.png)

下一题，看不懂了

```
Definition sillyfun1 (n : nat) : bool :=
  if beq_nat n 3 then true
  else if beq_nat n 5 then true
  else false.

Theorem sillyfun1_odd : forall (n : nat),
     sillyfun1 n = true ->
     oddb n = true.
Proof.
  intros n eq. unfold sillyfun1 in eq.
  destruct (beq_nat n 3) eqn:Heqe3.
    - (* e3 = true *) apply beq_nat_true in Heqe3.
      rewrite -> Heqe3. reflexivity.
    - destruct (beq_nat n 5) eqn:Heqe5.
        + apply beq_nat_true in Heqe5.
          rewrite -> Heqe5. reflexivity.
        + discriminate eq.  Qed.
```

下一个练习，完全tm看不懂

更新：看懂了，不难，主要就是布尔和函数有各种情况要分！

```
Theorem bool_fn_applied_thrice :
  forall (f : bool -> bool) (b : bool),
  f (f (f b)) = f b.
Proof.
  intros f b.
  destruct b.
  - destruct (f true) eqn:H1.
    + rewrite -> H1.  apply H1.
    + destruct (f false) eqn:H2.
      * apply H1.
      * apply H2.
  - destruct (f false) eqn:H3.
    + destruct (f true) eqn:H4.
      * apply H4.
      * apply H3.
    + rewrite -> H3. apply H3.
Qed.
```

## **本章可用的定理**

```
f_equal : x = y -> f x = f y
trans_eq :  n = m -> m = o -> n = o.
beq_nat_true : beq_nat n 3 = true → n=3
```

# **六、LOGIC**

## **6.2 逻辑连接词**

### **合取**

写作 A ∧ B，表示一个 A 与 B 均为真的断言

```
Example and_example : 3 + 4 = 7 ∧ 2 × 2 = 4.
```

证明合取的命题通常使用 **split 策略**。它会分别为语句的两部分生成两个子目标

```
Proof.
  split.
  - (* 3 + 4 = 7 *) reflexivity.
  - (* 2 * 2 = 4 *) reflexivity.
Qed.
```

由于按照前提对某个目标应用定理会产生与该定理的前提一样多的子目标

因此我们可以应用 and_intro 来达到和 split 一样的效果。

```
Lemma and_intro : forall A B : Prop, A -> B -> A /\ B.
Proof.
  intros A B HA HB. split.
  - apply HA.
  - apply HB.
Qed.

Example and_example' : 3 + 4 = 7 /\ 2 * 2 = 4.
Proof.
  apply and_intro.
  - (* 3 + 4 = 7 *) reflexivity.
  - (* 2 + 2 = 4 *) reflexivity.
Qed.
```

对于任意命题 A 和 B，如果我们假设 A 为真且 B 为真， 那么就能得出 A ∧ B 也为真的结论

```
Lemma and_intro : forall A B : Prop, A -> B -> A /\ B.
Proof.
  intros A B HA HB. split.
  - apply HA.
  - apply HB.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211223153913.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211223153924.png)

```
Example and_exercise :
  forall n m : nat, n + m = 0 -> n = 0 /\ m = 0.
Proof.
  intros [][].
  - (* n = O, m = O *) apply and_intro. reflexivity.
  - (* n = O, m = S m' *) apply and_intro. reflexivity.
  - (* n = S n', m = O *) split.
    + inversion H.
    + inversion H.
  - (* n = S n', m = S m' *) split.
    + inversion H.
    + inversion H.
Qed.
```

以上就是证明合取语句的方法。要反过来使用，即用合取前提来帮助证明时，采用 **destruct 策略**

```
Lemma and_example2 :
  forall n m : nat, n = 0 /\ m = 0 -> n + m = 0.
Proof.
  intros n m [Hn Hm].
  rewrite -> Hn. rewrite -> Hm.
  reflexivity.
Qed.
```

合取语句例子

```
Lemma and_example3 :
  forall n m : nat, n + m = 0 -> n * m = 0.
Proof.
  intros n m H.
  assert (H' : n = 0 /\ m = 0).
  { apply and_exercise. apply H. }
  destruct H' as [Hn Hm].
  rewrite Hn. reflexivity.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211223160036.png)

合取交换律

```
Theorem and_commut : forall P Q : Prop,
  P /\ Q -> Q /\ P.
Proof.
  intros P Q [HP HQ].
  split.
    - (* left *) apply HQ.
    - (* right *) apply HP.  Qed.
```

合取结合律

```
Theorem and_assoc : forall P Q R : Prop,
  P /\ (Q /\ R) -> (P /\ Q) /\ R.
Proof.
  intros P Q R [HP [HQ HR]].
  split.
  - (* P /\ Q *) split.
    + apply HP.
    + apply HQ.
  - (* /\ R *) apply HR.
Qed.
```

**练习**

没看懂

```
Example and_exercise :
  forall n m : nat, n + m = 0 -> n = 0 /\ m = 0.
Proof.
  intros [][].
  - (* n = O, m = O *) apply and_intro. reflexivity.
  - (* n = O, m = S m' *) apply and_intro. reflexivity.
  - (* n = S n', m = O *) split.
    + inversion H.
    + reflexivity.
  - (* n = S n', m = S m' *) split.
    + inversion H.
    + inversion H.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211223154414.png)

自己改了下，能看懂了

```
Example and_exercise :
  forall n m : nat, n + m = 0 -> n = 0 /\ m = 0.
Proof.
  intros [][].
  - (* n = O, m = O *) split.  + reflexivity. + reflexivity.
  - (* n = O, m = S m' *) split. + reflexivity. + inversion H.
  - (* n = S n', m = O *) split.
    + inversion H.
    + inversion H.
  - (* n = S n', m = S m' *) split.
    + inversion H.
    + inversion H.
Qed.
```

### **析取**

若 A 或 B 二者之一为真，则 A ∨ B 为真

可以显式地通过 **destruct** 或隐式地通过 intros 模式来拆分

```
Lemma or_example :
  forall n m : nat, n = 0 \/ m = 0 -> n * m = 0.
Proof.
  intros n m [Hn | Hm].
  - (* Here, [n = 0] *)
    rewrite Hn. reflexivity.
  - (* Here, [m = 0] *)
    rewrite Hm. rewrite <- mult_n_O.
    reflexivity.
Qed.

```

要证明某个析取命题成立，只需证明其任意一边的命题成立就够了

**left 和 right 策略**来选取命题

```
Lemma or_intro : forall A B : Prop, A -> A \/ B.
Proof.
  intros A B H.
  left.
  apply H.
Qed.
```

因为析取是只要一边满足就行了，这里用left和right来指明满足的是哪一边

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226182719.png)

```
Lemma zero_or_succ :
  forall n : nat, n = 0 \/ n = S (pred n).
Proof.
  intros [|n].
  - left. reflexivity.
  - right. reflexivity.
Qed.
```

```
Lemma mult_eq_0 :
  forall n m, n * m = 0 -> n = 0 \/ m = 0.
Proof.
  intros [|n].
  - left. reflexivity.
  - right. destruct m as [|m'].
    + reflexivity.
    + inversion H.
Qed.
```

下面这个完全看不懂，inversion是什么，保留疑问

```
Theorem or_commut : forall P Q : Prop,kkkkkkkkkkkkkkkkkkkkkk
  P \/ Q  -> Q \/ P.
Proof.
  intros P Q H.
  inversion H.
  - right. apply H0.
  - left. apply H0.
Qed.
```

### **假命题与否定**

将 ¬ P 定义为 P → False，而 False 是在标准库中特别定义的矛盾性命题

由于 False 是个矛盾性命题，因此爆炸原理对它也适用

如果我们让 False 进入到了证明的上下文中，可以对它使用 destruct 来完成任何待证目标

（咱就是完全没看懂）

```
Theorem ex_falso_quodlibet : forall (P:Prop),
  False -> P.
Proof.
  intros P contra.
  destruct contra.  Qed.
```

**练习**

```
Fact not_implies_our_not : forall (P:Prop),
  ~ P -> (forall (Q:Prop), P -> Q).
Proof.
  intros P H Q H0.
  destruct H.
  apply H0.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211223163634.png)

咱就是说没看懂啊，为什么destruct一下Q就变成P了

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226163338.png)

**练习2**

unfold not 可以把 ~P 改写为 P -> false

```
Theorem zero_not_one : ~(0 = 1).
Proof.
  unfold not.
  intros H.
  discriminate H.
Qed.
```

**练习3**

过程倒是都看懂了，就是不知道为什么这么就证完了？

```
Theorem contradiction_implies_anything : forall P Q : Prop,
  (P /\ ~P) -> Q.
Proof.
  intros P Q [HP HNA].
  unfold not in HNA.
  apply HNA in HP.
  destruct HP.
  Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226165114.png)

不是要证明Q吗？没懂啊

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226165153.png)

**练习4**

大概看懂了就是没看懂 apply H0那一步

```
Theorem double_neg : forall P : Prop,
  P -> ~~P.
Proof.
  intros P H.
  unfold not.
  intros H0.
  apply H0.
  apply H.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226165510.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226165523.png)

apply是可以从结论推出条件吗？

**练习5**

这道题我自己做的哈哈啊哈，就根据右边的提示一步一步来就好

```
Theorem contrapositive : forall (P Q : Prop),
  (P -> Q) -> (~Q -> ~P).
Proof.
  unfold not.
  intros P Q H.
  intros H1 H2.
  apply H1.
  apply H.
  apply H2.
Qed.
```

**练习6**

也是我自己做的，仿佛已经掌握了哈哈哈

```
Theorem not_both_true_and_false : forall P : Prop,
  ~ (P /\ ~P).
Proof.
  unfold not.
  intros P.
  intros [H1 H2].
  apply H2.
  apply H1.
Qed.
```

**练习7**

补充：爆炸定理

```
ex_falso_quodlibet
     : forall P : Prop, False -> P
```

```
Theorem not_true_is_false : forall b : bool,
  b <> true -> b = false.
Proof.
  intros [] H.
  - (* b = true *)
    unfold not in H.
    apply ex_falso_quodlibet.
    apply H. reflexivity.
  - (* b = false *)
    reflexivity.
Qed.
```

由于用 ex_falso_quodlibet 推理十分常用，因此 Coq 提供了内建的策略 **exfalso**

```
Theorem not_true_is_false' : forall b : bool,
  b <> true -> b = false.
Proof.
  intros [] H.
  - (* b = true *)
    unfold not in H.
    exfalso.
    apply H. reflexivity.
  - (* b = false *) reflexivity.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226171700.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226171715.png)

怎么化的啊？没懂again

### **真值**

不常用，用到再来看

### **逻辑等价**

当且仅当，充分必要条件

```
Definition iff (P Q : Prop) := (P -> Q) /\ (Q -> P).

Notation "P <-> Q" := (iff P Q)
                      (at level 95, no associativity)
                      : type_scope.
```

**例题**

```
Theorem iff_sym : forall P Q : Prop,
  (P <-> Q) -> (Q <-> P).
Proof.
  intros P Q [HAB HBA].
  split.
  - apply HBA.
  - apply HAB.  Qed.
```

**例题2**

```
Lemma not_true_iff_false : forall b,
  b <> true <-> b = false.
Proof.
  intros b.
  split.
  - apply not_true_is_false.
  - unfold not.
    intros H.
    rewrite H.
    intros H2.
    inversion H2.
Qed.
```

**例题3**

```
Theorem iff_trans : forall P Q R : Prop,
  (P <-> Q) -> (Q <-> R) -> (P <-> R).
Proof.
  intros P Q R [H1 H2].
  intros [H3 H4].
  split.
  - intros H5.
    apply H3.
    apply H1.
    apply H5.
  - intros H6.
    apply H2.
    apply H4.
    apply H6.
Qed.
```

**例题4⭐️**

一定要注意这种引入条件拆分的语法

条件为 kkk P \/ (Q /\ R) ：intros [H1|[H2 H3]].

条件为 (P \/ Q) /\ (P \/ R)：intros[[H1|H2] [H3|H4]].

```
Theorem or_distributes_over_and : forall P Q R : Prop,
  P \/ (Q /\ R) <-> (P \/ Q) /\ (P \/ R).
Proof.
  intros P Q R.
  split.
  - intros [H1|[H2 H3]].
     + split.
        * left. apply H1.
        * left. apply H1.
     + split.
        * right. apply H2.
        * right. apply H3.
  - intros[[H1|H2] [H3|H4]].
    +left. apply H1.
    +left. apply H1.
    +left. apply H3.
    +right. split.
      * apply H2.
      * apply H4.
Qed.
```

### **广集**

导入库

```
Require Import Coq.Setoids.Setoid.
```

广集（Setoid）指配备了等价关系的集合，即满足自反性、对称性和传递性的关系

当一个集合中的两个元素在这种关系上等价时，可以用 rewrite 将其中一个元素替换为另一个

逻辑等价关系 ↔ 也满足自反性、对称性和传递性，因此若 P ↔ Q，那么我们可以用 rewrite 将 P 替换为 Q

为了复习之前的知识先做两个证明

```
Check mult_eq_0.
Lemma mult_0 : forall n m, n * m = 0 <-> n = 0 \/ m = 0.
Proof.
  split.
  - apply mult_eq_0.
  - apply or_example.
Qed.

Lemma or_assoc :
  forall P Q R : Prop, P \/ (Q \/ R) <-> (P \/ Q) \/ R.
Proof.
  intros P Q R. split.
  - intros [H | [H | H]].
    + left. left. apply H.
    + left. right. apply H.
    + right. apply H.
  - intros [[H | H] | H].
    + left. apply H.
    + right. left. apply H.
    + right. right. apply H.
Qed.
```

现在我们可以配合这两个证明和rewrite证明下面的东西

```
Lemma mult_0_3 :
  forall n m p, n * m * p = 0 <-> n = 0 \/ m = 0 \/ p = 0.
Proof.
  intros n m p.
  rewrite mult_0. rewrite mult_0. rewrite or_assoc.
  reflexivity.
Qed.
```

apply关系也可以用在逻辑蕴含上

```
Lemma apply_iff_example :
  forall n m : nat, n * m = 0 -> n = 0 \/ m = 0.
Proof.
  intros n m H. apply mult_0. apply H.
Qed.
```

### **存在量化**

**exists t 策略** 指出已经知道了使 P 成立的例子 t

```
Lemma four_is_even : exists n : nat, 4 = n + n.
Proof.
  exists 2. reflexivity.
Qed.
```

找到例子t之后把所有出现的x换成t代入

```
Theorem exists_example_2 : forall n,
  (exists m, n = 4 + m) ->
  (exists o, n = 2 + o).
Proof.
  intros n [m Hm].    // Hm : n = 4 + m
  exists (2 + m).     // n = 2 + (2 + m)
  apply Hm.  Qed.
```

**练习1**

**destruct H as [x E] 可以用于存在假设！**

```
Theorem dist_not_exists : forall (X:Type) (P : X -> Prop),
  (forall x, P x) -> ~ (exists x, ~ P x).
Proof.
  intros X P H.
  unfold not.
  intros [x H2].
  destruct H2.
  apply H.
Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226202215.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226202230.png)

**练习2**

```
Theorem dist_exists_or : forall (X:Type) (P Q : X -> Prop),
  (exists x, P x \/ Q x) <-> (exists x, P x) \/ (exists x, Q x).
Proof.
  intros X P Q.
  split.
  - intros [n [H1|H2]].
    +left. exists n. apply H1.
    +right. exists n. apply H2.
  - intros [[n H1]|[n H2]].
    +exists n. left. apply H1.
    +exists n. right. apply H2.
Qed.
```

要注意的是 intro 的时候要对应！

(exists x : X, P x \/ Q x)：[n [H1|H2]]

(exists x : X, P x) \/ (exists x : X, Q x)：[[n H1]|[n H2]]

还有注意apply和exists的顺序

(exists x : X, P x) \/ (exists x : X, Q x)： left. exists n. apply H1.

exists x : X, P x \/ Q x：exists n. left. apply H1.

## **6.3 使用命题编程**

判断一个元素在不在列表中

```
Fixpoint In {A : Type} (x : A) (l : list A) : Prop :=
  match l with
  | [] => False
  | x' :: l' => x' = x \/ In x l'
  end.
```

当 In 应用于具体的列表时，它会被展开为一系列具体的析取式

```
Example In_example_1 : In 4 [1; 2; 3; 4; 5].
Proof.
  simpl.   //1 = 4 \/ 2 = 4 \/ 3 = 4 \/ 4 = 4 \/ 5 = 4 \/ False
  right.   //2 = 4 \/ 3 = 4 \/ 4 = 4 \/ 5 = 4 \/ False
  right.   //3 = 4 \/ 4 = 4 \/ 5 = 4 \/ False
  right.   //4 = 4 \/ 5 = 4 \/ False
  left.    //4 = 4
  reflexivity.
Qed.
```

**练习**

intros的时候多加注意呀！

```
Example In_example_2 :
  forall n, In n [2; 4] ->
  exists n', n = 2 * n'.
Proof.
  (* WORKED IN CLASS *)
  simpl.
  intros n [H1 | [H2 | []]].
  - exists 1. rewrite <- H1. reflexivity.
  - exists 2. rewrite <- H2. reflexivity.
Qed.
```

首先 In 会被应用到一个变量上，只有当我们对它进行分类讨论时， 它才会被展开

```
Lemma In_app_iff : forall A l1 l2 (a:A),
  In a (l1 ++ l2) <-> In a l1 \/ In a l2.
Proof.
  intros A l1 l2 a.
  split.
  - (* -> *) intro H.
    induction l1 as [|n l1' IHl1].
    + (* l1 = nil *) simpl in H. right. apply H.
    + (* l1 = n :: l1' *) simpl in H.
      destruct H as [H1 | H2].
      * left. simpl. left. apply H1.
      * apply IHl1 in H2. simpl. apply or_assoc. right. apply H2.
  - (* <- *) intro H.
    induction l1 as [|n l1' IHl1].
    + simpl. destruct H.
      * inversion H.
      * apply H.
    + simpl in H.
      apply or_assoc in H. destruct H as [H1 | H2].
      * simpl. left. apply H1.
      * apply IHl1 in H2. simpl. right. apply H2.
Qed.
```

**练习**

定义一个关系对列表中所有的元素都成立

```
Fixpoint All {T : Type} (P : T -> Prop) (l : list T) : Prop :=
  match l with
  | nil => True
  | h :: t => P h /\ All P t
  end.
```

证明

总结了一些

1. 看到蕴含关系就split
2. 看到 In 加列表就 induction

```
Lemma All_In :
  forall T (P : T -> Prop) (l : list T),
    (forall x, In x l -> P x) <->
    All P l.
Proof.
  intros T P l.
  split.
  - (* -> *) intros H.
    induction l as [|n' l' IHl].
    + (* l = nil *) reflexivity.
    + (* l = n :: l' *) simpl. split. (*P n' /\ All P l'*)
      * apply H. simpl. left. reflexivity.
      * apply IHl. intros x H1. apply H. simpl. right. apply H1.
  - (* <- *) intros H. induction l as [|n l' IHl].
    + intros x H0. inversion H0.
    + simpl. intros x H0. destruct H0.
      * simpl in H. apply proj1 in H. rewrite <- H0. apply H.
      * simpl in H. apply proj2 in H. apply IHl with x in H.
        { apply H. }
        { apply H0. }
Qed.
```

好他妈难啊，不想学了

## **6.3 可以用的定理**

```
and_intro : A -> B -> A /\ B.
and_exercise : n + m = 0 -> n = 0 /\ m = 0.
and_example2 : n = 0 /\ m = 0 -> n + m = 0.
```

# **七、归纳定义的命题**

## **7.1 偶数性的归纳定义**

为了理解这个新的偶数性质定义如何工作，我们可想象如何证明 4 是偶数。 根据规则 ev_SS，需要证明 2 是偶数。这时，只要证明 0 是偶数， 我们可继续通过规则 ev_SS 确保它成立。而使用规则 ev_0 可直接证明 0 是偶数

基于上述，可将偶数性质的定义翻译为在 Coq 中使用 Inductive 声明的定义， 声明中每一个构造子对应一个推断规则：

```
Inductive ev : nat -> Prop :=
| ev_0 : ev 0
| ev_SS : forall n : nat, ev n -> ev (S (S n)).
```

可以用apply来证明

```
Theorem ev_4 : ev 4.
Proof. apply ev_SS. apply ev_SS. apply ev_0. Qed.
```

```
Theorem ev_4' : ev 4.
Proof. apply (ev_SS 2 (ev_SS 0 ev_0)). Qed.
```

```
Theorem ev_plus4 : forall n, ev n -> ev (4 + n).
Proof.
  intros n. simpl. intros Hn.
  apply ev_SS. apply ev_SS. apply Hn.
Qed.
```

证明任何数乘以2都是偶数

```
Theorem ev_double : forall n,
  ev (double n).
Proof.
  induction n as [|n' IHn].
  - apply ev_0.
  - simpl. apply ev_SS. apply IHn.
Qed.
```

## **7.2 在证明中使用证据**

### **对证据进行反演**

可以使用 destruct 来证明我们对 ev n 的证据特征

- E is ev_0(and n is 0)
- E is ev_SS n' E' (and n is S (S n)), E' is the evidence for even n'

证明任意偶数减2都是偶数

```
Theorem ev_minus2 : forall n,
  ev n -> ev (pred (pred n)).
Proof.
  intros n E.
  destruct E as [| n' E'].
  - (* E = ev_0 *) simpl. apply ev_0.
  - (* E = ev_SS n' E' *) simpl. apply E'.  Qed.
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211226231636.png)

```
Theorem evSS_ev : forall n,
  ev (S (S n)) -> ev n.
Proof.
  intros n E.
  inversion E as [| n' E'].
  (* We are in the [E = ev_SS n' E'] case now. *)
  apply E'.
Qed.
```

### **对证明进行归纳**

## **7.3 归纳关系**

和和

# **八、关系的性质**

集合 X 上的二元*'关系（Relation）'*指所有由两个 X 中的元素参数化的命题， 即，有关一对 X 中的元素的命题。

## **偏函数**

对于集合 X 上的关系 R ，如果对于任何 x 最多只有一个 y 使得 R x y 成立 -- 即，R x y1 和 R x y2 同时成立蕴含 y1 = y2， 则称 R 为'偏函数

# **九、期末考试题**

## **简单证明**

1.mul_2_r

```
Theorem my : forall n m: nat,
  S (n + m + 2) = n + S m + 2.
Proof.
  intros n m.
  induction n as [| n' IHn'].
  - simpl. reflexivity.
  - simpl. rewrite <- IHn'. reflexivity.
Qed.

Lemma mul_2_r : forall  n : nat,
  (n + 1) * 2 = n + n + 2.
Proof.
  intros n.
  induction n as [| n' IHn'].
  - simpl. reflexivity.
  - simpl. rewrite IHn'. rewrite my. reflexivity.
Qed.
```

2.mult_3_r

```
Theorem plus_n_Sm : forall n m : nat,
  S (n + m) = n + (S m).
Proof.
  intros n m.
  induction n as [| n' IHn'].
  - simpl. reflexivity.
  - simpl. rewrite IHn'. reflexivity.
Qed.

Theorem buchong: forall n m p:nat,
S(S(n+m+p))=n+(S m)+(S p).
Proof.
intros n m p. induction n as[|n' xs].
-simpl. rewrite plus_n_Sm.  reflexivity.
-simpl. rewrite xs. reflexivity.
Qed.

Lemma mul_3_r : forall n : nat, n * 3 = n + n + n.
Proof.
intros n.
induction n.
-simpl. reflexivity.
-simpl. rewrite IHn. rewrite buchong. reflexivity.
Qed.
```

## **递归定义**

1.div2021

```
Fixpoint div2021 (n : nat ) : bool :=
 match n with
  | O => true
  | S n' => match leb n 2020 with
    | true => false
    | false => div2021 (n'-2020)
    end
 end.

Example div2021_test0: div2021 2020 = false.
Proof. reflexivity. Qed.

Example div2021_test1: div2021 4042 = true.
Proof. reflexivity. Qed.

Example div2021_test2: div2021 2027 = false.
Proof. reflexivity. Qed.
```

2.div5

```
Fixpoint div5 (n : nat) : bool :=
match n with
  |0 => true
  |1 => false
  |2 => false
  |3 => false
  |4 => false
  |S (S (S (S (S n')))) => div5 n'
end.
```

3.关于奇数和偶数

```
Fixpoint evenb (n: nat) : bool :=
match n with
|0 => true
|1 => false
|S (S n') => evenb n'
end.

Definition oddb (n:nat) : bool :=
  negb (evenb n).
```

4.square（还没做出来）

```
Definition squared (n : nat) : bool :=
  (* FILL IN HERE *) admit.

Example square_test1 : squared 8 = false.
Proof. (* FILL IN HERE *)
Admitted.

Example square_test2 : squared 25 = true.
Proof. (* FILL IN HERE *)
Admitted.

```

## **逻辑证明**

```
Definition excluded_middle := forall P : Prop,
  P \/ ~ P.

Definition peirce := forall P Q: Prop,
  ((P->Q)->P)->P.

Definition double_negation_elimination := forall P:Prop,
  ~~P -> P.

Definition de_morgan_not_and_not := forall P Q:Prop,
  ~(~P /\ ~Q) -> P\/Q.

Definition implies_to_or := forall P Q:Prop,
  (P->Q) -> (~P\/Q).
```

```
Theorem peirce_valid : excluded_middle <-> peirce.
Proof.
  split.
  - (* -> *) intros E P Q.
    intro H. destruct (E P) as [H'|H'].
    + apply H'.
    + apply H. intro HP. exfalso. apply H'. apply HP.
  - (* <- *) intros E H.
    apply (E (H \/ ~H) False).
    intro H1.
    apply excluded_middle_irrefutable in H1.
    inversion H1.
Qed.
```

```
Theorem double_negation_elimination_valid :
  excluded_middle <-> double_negation_elimination.
Proof.
  split.
  - (* -> *) intros E P.
    destruct (E P) as [H' | H'].
    + intro HP. apply H'.
    + intro HNP.
      unfold not in H'.
      unfold not in HNP.
      apply HNP in H'.
      inversion H'.
  - (* <- *) intros DNE EXM.
    apply DNE. apply excluded_middle_irrefutable.
Qed.
```

```
Theorem de_morgan_not_and_not_valid :
  excluded_middle <-> de_morgan_not_and_not.
Proof.
  split.
  - (* -> *) intros E P Q.
    destruct (E P) as [HP | HP].
    + intro H. left. apply HP.
    + destruct (E Q) as [HQ | HQ].
      * intro H. right. apply HQ.
      * intro H. exfalso. apply H. split.
        { apply HP. }
        { apply HQ. }
  - (* <- *) intros D E.
    apply D.
    unfold not.
    intros [H1 H2].
    apply H2. apply H1.
Qed.
```

```
Theorem implies_to_or_valid :
  excluded_middle <-> implies_to_or.
Proof.
  split.
  - (* -> *) intros E P Q.
    destruct (E P) as [HP | HP].
    + intro H. right. apply H. apply HP.
    + intro H. left. apply HP.
  - (* <- *) intros IO E.
    rewrite -> or_comm. apply IO. intro HE. apply HE.
Qed.
```

**发现两年的考试题都是书上最后的原题：**

```
Theorem excluded_middle :
  (forall P Q : Prop, (P -> Q) -> (~P \/ Q)) -> (forall P, P \/ ~P).
Proof.
  intros IO E.
  rewrite -> or_comm. apply IO. intro HE. apply HE.
Qed.
```

```
Theorem de_morgan :
   (forall P, P \/ ~P) -> (forall P Q, ~(~P /\ ~Q) -> P \/Q).
Proof.
    intros E P Q.
    destruct (E P) as [HP | HP].
    + intro H. left. apply HP.
    + destruct (E Q) as [HQ | HQ].
      * intro H. right. apply HQ.
      * intro H. exfalso. apply H. split.
        { apply HP. }
        { apply HQ. }
Qed.
```

## **列表相关**

**一、构造列表**

1.Define a function createList such that (createList n) returns  a list of numbers in the form:

**[n;(n-1);...;2;1;2;...;(n-1);n]**

```
Fixpoint createList1 (n : nat) : list nat :=
match n with
| 0 => nil
| S n' =>  (createList1 n') ++[n]
end.

Fixpoint createList2 (n : nat) : list nat :=
match n with
| 0 => nil
| 1 => nil
| S n' => [n] ++ (createList2 n')
end.

Definition createList (n : nat) : list nat :=
(createList2 n )++(createList1 n).

Example createList_test : createList 6 = [6;5;4;3;2;1;2;3;4;5;6].
Proof. reflexivity. Qed.
```

2.Let two sequences of numbers F1(n) and F2(n) be given as follows.

F1(0) = 0

F1(n) = F1(n-1) + 2 * n   for n > 0.

F2(0) = F2(1) = 1

F2(n+2) = F2(n) + F2(n+1)    for n >= 0.

Define the function Seq such that (Seq n) returns the sequence

**[F1(0); F2(0); F1(1); F2(1); ... ; F1(n); F2(n)].**

```
Notation "x :: l" := (cons x l)
                     (at level 60, right associativity).
Notation "x ++ y" := (app x y)
                     (right associativity, at level 60).

Fixpoint feb1 (n:nat) : nat :=
  match n with
  | O => 0
  | S n' => (feb1 n') + 2*n
  end.

Fixpoint feblist1 (n : nat) : list nat :=
  match n with
  | O => [0]
  | S n' => (feblist1 n') ++ [feb1 n]
  end.

Fixpoint feb2 (n:nat) : nat :=
  match n with
  | O => 1
  | S O => 1
  | S n' => feb2 n' + feb2 (n'-1)
  end.

Fixpoint feblist2 (n : nat) : list nat :=
  match n with
  | O => [1]
  | S O => [1;1]
  | S n' => (feblist2 n') ++ [feb2 n]
  end.

Fixpoint alternate (l1 l2 : list nat) : list nat :=
  match l1 with
  | nil => l2
  | h1 :: t1 => match l2 with
            | nil => l1
            | h2 :: t2 => h1 :: h2 :: (alternate t1 t2)
            end
  end.

Definition Seq (n: nat) : list nat :=
 alternate (feblist1 n) (feblist2 n).

Example Seq_test :  Seq 5 = [0; 1; 2; 1; 6; 2; 12; 3; 20; 5; 30; 8].
Proof. reflexivity. Qed.
```

**二、过滤器**

1.which partitions a list into a list of 3 sublists. The first sublist
   contains all even numbers in the original list. The second sublist 
   contains all odd numbers divisible by 5 in the original list. The last 
   sublist contains all other elements. The order of elements in the
   three sublists should be the same as their order in the original list.

```

Search filter.
Fixpoint evenb (n: nat) : bool :=
match n with
|0 => true
|1 => false
|S (S n') => evenb n'
end.

Fixpoint div5 (n : nat) : bool :=
match n with
  |0 => true
  |1 => false
  |2 => false
  |3 => false
  |4 => false
  |S (S (S (S (S n')))) => div5 n'
end.

Definition find (l: nat) : bool :=
match orb (evenb l) (div5 l)  with
|true => false
|false => true
end.

Definition partition (l : list nat) : list (list nat) :=
[filter evenb l] ++ [filter div5 l] ++ [filter find l].

Compute partition [1;2;3;9;4;5;6;15;8;10].

Example partition_test: partition [1;2;3;9;4;5;6;15;8] = [[2;4;6;8]; [5;15]; [1;3;9]].
Proof. reflexivity. Qed.
```

2.which partitions a list into a list of 3 sublists. The first sublist
   contains all odd numbers divisible by 3 in the original list. 
   The second sublist contains all other odd numbers in the original list. 
   The last sublist contains all the even numbers in the original list. 
   The order of elements in the three sublists should be the same as their 
   order in the original list.

```
Fixpoint evenb (n: nat) : bool :=
match n with
|0 => true
|1 => false
|S (S n') => evenb n'
end.

Definition oddb (n:nat) : bool :=
  negb (evenb n).

Fixpoint div3 (n : nat) : bool :=
match n with
  |0 => true
  |1 => false
  |2 => false
  |S (S (S n')) => div3 n'
end.

Definition find1 (l: nat) : bool :=
match andb (oddb l) (div3 l)  with
|true => true
|false => false
end.

Definition find2 (l: nat) : bool :=
match andb (oddb l) (negb(div3 l))  with
|true => true
|false => false
end.

Definition partition (l : list nat) : list (list nat) :=
[filter find1 l] ++ [filter find2 l] ++ [filter evenb l].

Compute partition [1;2;3;9;4;5;6;15;21;8;7].

Example partition_test:
  partition [1;2;3;9;4;5;6;15;8] = [[3; 9; 15]; [1; 5]; [2; 4; 6; 8]].
Proof. reflexivity. Qed.

```

三、复杂的列表操作

1.旋转

```
Fixpoint rotate1 (l : list nat) : list nat :=
(* FILL IN HERE *)
match l with
| nil => nil
| h::t => match t with
         | nil => [h]
         | h' :: t' => rotate1 t
         end
end.

Compute rotate1 [1;2;3;4;5].

Fixpoint rotate2 (l : list nat) : list nat :=
(* FILL IN HERE *)
match l with
| nil => nil
| h::t => match t with
         | nil => nil
         | h' :: t' => [h] ++ rotate2 t
         end
end.

Definition rotate (l : list nat) : list nat :=
(* FILL IN HERE *)
match l with
| nil => nil
| h::t => rotate1 l ++ rotate2 l
end.

Compute  rotate [1;2;3;4;5].

Example rotate_test : rotate [1;2;3;4;5] = [5;1;2;3;4].
Proof. reflexivity. Qed.
```

2.交换第一个数和最后一个数

```
Definition swap2 (l : list nat) : list nat :=
  match l with
  | nil => nil
  | h::t => match rev t with
            | nil => [h]
            | h'::t' => h'::rev t'++[h]
            end
  end.

Compute rev [1;2;3].
```

3.交换最大的数和最小的数

```

```

4.数列排序

```
Fixpoint insert(x:nat)(l:list nat):list nat:=
  match l with
  | nil => [x]
  | a::t => match leb x a with
            | true => x::l
            | false => a::insert x t
            end
  end.

Compute insert 7 [3;6;5].

Fixpoint sort(l:list nat):list nat:=
  match l with
  | nil => nil
  | h::t => insert h (sort t)
  end.

Compute sort [3;7;2;5;1;4;6].
Example sort_test : sort [3;7;2;5;1;4;6] = [1;2;3;4;5;6;7].
Proof. reflexivity. Qed.
```

## **二叉树**

1.Define a function taking as argument a tree t: btree and returning the **sum of all numbers** occurring in the tree.

```
Inductive btree : Set :=
 | leaf : nat -> btree
 | node : nat -> btree -> btree -> btree.

Fixpoint sum (t: btree) : nat :=
  match t with
    | leaf a=>a
    | node h f e => h + sum f + sum e
  end.

Example bt_test : sum (node 5 (node 1 (leaf 0) (node 3 (leaf 2) (leaf 4)))
                              (node 9 (node 7 (leaf 6) (leaf 8)) (leaf 10)))
                  = 55.
Proof. reflexivity. Qed.
```

2.Define a function to give a **preorder traversal** of the tree and collect all the odd numbers in a list.

```
Inductive btree : Set :=
 | leaf : nat -> btree
 | node : nat -> btree -> btree -> btree.

Fixpoint preorder (t: btree) : list nat :=
  match t with
    | leaf a => [a]
    | node h f e => [h] ++ preorder f ++ preorder e
  end.

Definition preorder2 (t: btree) :  list nat :=
  filter oddb (preorder t).

Example bt_test : preorder2 (node 5 (node 1 (leaf 0) (node 3 (leaf 2) (leaf 4)))
                                   (node 9 (node 7 (leaf 6) (leaf 8)) (leaf 10)))
                   = [5; 1; 3; 9; 7].
Proof. reflexivity. Qed.
```

3.**postorder traversal**

```
Fixpoint postorder (t: btree) : list nat :=
  match t with
    | leaf a => [a]
    | node h f e =>  postorder f ++ postorder e ++ [h]
  end.

Compute postorder (node 5 (node 1 (leaf 0) (node 3 (leaf 2) (leaf 4)))
                                   (node 9 (node 7 (leaf 6) (leaf 8)) (leaf 10))).

```

## **优化**

```

```

# **函数式程序语言设计 examB**

张彩仪 10184602316

2022/2/18

## **第一题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105644.png)

## **第二题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105702.png)

## **第三题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105728.png)

## **第四题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105748.png)

## **第五题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105813.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105823.png)

## **第六题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105842.png)

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105857.png)

## **第七题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105914.png)

## **第八题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105928.png)

## **第九题**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220218105943.png)

## **第十题**

```
(* 10. The following definitions specify the abstract syntax of
    some arithmetic expressions and an evaluation function. *)

Inductive aexp : Type :=
  | ANum : nat -> aexp
  | APlus : aexp -> aexp -> aexp
  | AMinus : aexp -> aexp -> aexp
  | AMult : aexp -> aexp -> aexp.

Fixpoint aeval (a : aexp) : nat :=
  match a with
  | ANum n => n
  | APlus a1 a2 => (aeval a1) + (aeval a2)
  | AMinus a1 a2 => (aeval a1) - (aeval a2)
  | AMult a1 a2 => (aeval a1) * (aeval a2)
  end.

(* Suppose we define a function that takes an arithmetic expression
   and slightly simplifies it, changing every occurrence of [e + 0]
   and [e - 0] into just [e], and [e * 1] into [e]. *)

Fixpoint optimize (a:aexp) : aexp :=
  match a with
  | ANum n => ANum n
  | APlus e2 (ANum 0) => optimize e2
  | APlus e1 e2 => APlus (optimize e1) (optimize e2)
  | AMinus e1 e2 => AMinus (optimize e1) (optimize e2)
  | AMult e2 (ANum 1)  => optimize e2
  | AMult e1 e2 => AMult (optimize e1) (optimize e2)
  end.

(* Prove the following theorem that states the correctness of the
optimization with respect to the evaluation of arithmetic expressions. *)

Theorem plus_n_O : forall n:nat, n = n + 0.
Proof.
  intros n. induction n as [| n' IHn'].
  - (* n = 0 *)    reflexivity.
  - (* n = S n' *) simpl. rewrite <- IHn'. reflexivity.  Qed.

Theorem mult_n_1 : forall n : nat,
  n = n*1.
Proof.
  intros n. induction n as [|n' js].
- reflexivity.
- simpl. rewrite <- js. reflexivity. Qed.
Theorem optimize_mult1_sound: forall a,
  aeval (optimize a) = aeval a.
Proof.
intros a. induction a.
- try simpl ;reflexivity.
-destruct a2.
  +destruct n.  {simpl. rewrite IHa1. apply plus_n_O with (n:= aeval a1). }
   {simpl. rewrite IHa1. reflexivity. }
  +assert(optimize (APlus a1 (APlus a2_1 a2_2)) = APlus (optimize a1) (optimize (APlus a2_1 a2_2)) ).
   {simpl. reflexivity. } rewrite H. assert(aeval (APlus (optimize a1) (optimize (APlus a2_1 a2_2))) =
  (aeval (optimize a1))+(aeval (optimize (APlus a2_1 a2_2)))). {simpl. reflexivity. }
  rewrite H0. rewrite IHa1. rewrite IHa2. simpl. reflexivity.
  +assert(optimize (APlus a1 (AMinus a2_1 a2_2)) = APlus (optimize a1) (optimize (AMinus a2_1 a2_2)) ).
   {simpl. reflexivity. }  rewrite H. assert(aeval (APlus (optimize a1) (optimize (AMinus a2_1 a2_2))) =
  (aeval (optimize a1))+(aeval (optimize (AMinus a2_1 a2_2)))). {simpl. reflexivity. }
  rewrite H0.  rewrite IHa1. rewrite IHa2. simpl. reflexivity.
  +assert(optimize (APlus a1 (AMult a2_1 a2_2)) = APlus (optimize a1) (optimize (AMult a2_1 a2_2)) ).
   {simpl. reflexivity. }  rewrite H. assert(aeval (APlus (optimize a1) (optimize (AMult a2_1 a2_2))) =
  (aeval (optimize a1))+(aeval (optimize (AMult a2_1 a2_2)))). {simpl. reflexivity. }
  rewrite H0.  rewrite IHa1. rewrite IHa2. simpl. reflexivity.
-simpl. rewrite IHa1. rewrite IHa2. reflexivity.
-destruct a2.
  +destruct n.
  simpl. rewrite IHa1. reflexivity.
  destruct n. {simpl. rewrite IHa1. apply mult_n_1 with (n:=aeval a1). }
  assert(optimize (AMult a1 (ANum (S(S n))))= AMult (optimize a1) (optimize (ANum (S(S n))))). { simpl. reflexivity. }
  rewrite H. assert(aeval (AMult (optimize a1) (optimize (ANum (S (S n)))))= (aeval (optimize a1))*(aeval (optimize (ANum (S(S n)))))).
  {simpl. reflexivity. }
  rewrite H0. simpl. rewrite IHa1. reflexivity.
  + assert(optimize (AMult a1 (APlus a2_1 a2_2))= AMult (optimize a1) (optimize (APlus a2_1 a2_2))).
    {simpl. reflexivity. } rewrite H.
    assert(aeval (AMult (optimize a1) (optimize (APlus a2_1 a2_2)))= (aeval (optimize a1))*(aeval (optimize (APlus a2_1 a2_2)))).
    {simpl. reflexivity. } rewrite H0. rewrite IHa2. rewrite IHa1. simpl. reflexivity.
  +assert(optimize (AMult a1 (AMinus a2_1 a2_2))= AMult (optimize a1) (optimize (AMinus a2_1 a2_2))).
    {simpl. reflexivity. } rewrite H.
    assert(aeval (AMult (optimize a1) (optimize (AMinus a2_1 a2_2)))= (aeval (optimize a1))*(aeval (optimize (AMinus a2_1 a2_2)))).
    {simpl. reflexivity. } rewrite H0. rewrite IHa2. rewrite IHa1. simpl. reflexivity.
  +assert(optimize (AMult a1 (AMult a2_1 a2_2))= AMult (optimize a1) (optimize (AMult a2_1 a2_2))).
    {simpl. reflexivity. } rewrite H.
    assert(aeval (AMult (optimize a1) (optimize (AMult a2_1 a2_2)))= (aeval (optimize a1))*(aeval (optimize (AMult a2_1 a2_2)))).
    {simpl. reflexivity. } rewrite H0. rewrite IHa2. rewrite IHa1. simpl. reflexivity.
Qed.
```