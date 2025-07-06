---
title: Java Input-Output
slug: Java-Input-Output
lastmod: 2025-07-01T00:00:00+00:00
---

之前刷 leetcode 都是核心代码模式

最近在准备面试发现不光要给出实现功能的函数，也要自己构造测试用例输入输出，稍微总结一下用法

## **输入格式**

两种输入格式，在读入数据量大的情况下，格式1的速度会快些

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

Scanner sc = new Scanner (new BufferedInputStream(System.in));
```

```java
import java.util.Scanner;
Scanner sc = new Scanner (System.in);
```

下面开始读取

```java
int n = sc.nextInt();
String s = sc.next(); //相当于 cin >> s;
double t = sc.nextDouble();
String s = sc.nextLine(); //相当于cin.getline(...);
```

判断是否有下一个输入

```java
sc.hasNext()
sc.hasNextInt()
sc.hasNextDouble()
sc.hasNextLine()
```

最后记得关闭输出流

```java
sc.close();
```

## **输出格式**

```java
System.out.print();
System.out.println();
System.out.format();
System.out.printf();
```

## **读入多个整数**

Input 输入数据有多组，每组占一行，由一个整数组成

```java
Sample Input
    56
    67
    100
    123

import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc =new Scanner(System.in);
        while(sc.hasNext()){ //判断是否结束
            int score = sc.nextInt();//读入整数
        }
    }
}
```

## **输入多组整数**

输入数据有多组，每组占2行，第一行为一个整数N，指示第二行包含N个实数

```java
Sample Input
4
56.9 67.7 90.5 12.8
5
56.9 67.7 90.5 12.8

import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc =new Scanner(System.in);
        while(sc.hasNext()){
            int n = sc.nextInt();
            for(int i=0;i<n;i++){
                double a = sc.nextDouble();
                。。。。。。
            }
        }
    }
}
```

## **输入字符串**

输入数据有多行，第一行是一个整数n，表示测试实例的个数，后面跟着n行，每行包括一个由字母和数字组成的字符串。

```java
Sample Input
2
asdfasdf1
asdf1111111

import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i=0;i<n;i++){
            String str = sc.next();
            ......
        }
    }
}
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = Integer.parseInt(sc.nextLine());
        for(int i=0;i<n;i++){
            String str = sc.nextLine();
            ......
        }
    }
}
```

## **输入链表**

链表的数据结构

```java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}
```

将要调用的初始链表函数如下

```java
public static ListNode InitListNode(int[] ints) {
    ListNode head = new ListNode(0);
    ListNode p = head;
    for (int i = 0; i < ints.length; i++) {
        p.next = new ListNode(ints[i]);
        p = p.next;
    }
    return head.next;
}
```

输入以逗号分隔的一串数字，比如1,2,3,4,5

```java
Scanner scanner = new Scanner(System.in);
String str = scanner.next().toString();
String[] arr = str.split(",");

int[] ints = new int[arr.length];
for (int j = 0; j < ints.length; j++) {
    ints[j] = Integer.parseInt(arr[j]);
}

//初始链表
ListNode head = InitListNode(ints);

scanner.close();
```

输出，也是以字符串隔开的数字

```java
while (myhead != null) {
    if (myhead.next == null) {
        System.out.print(myhead.val);
    } else {
        System.out.print(myhead.val + ",");
    }
    myhead = myhead.next;
}
```

下面用反转链表举个例子，怎么将leetode中我们写好的核心代码融入输入输出中

注意如果main里面要调用该类的方法和类，要用static修饰，否则会报错

```java
import java.util.Scanner;

class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

public class ReverseList {

    public static ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }

    public static ListNode InitListNode(int[] ints) {
        ListNode head = new ListNode(0);
        ListNode p = head;
        for (int i = 0; i < ints.length; i++) {
            p.next = new ListNode(ints[i]);
            p = p.next;
        }
        return head.next;
    }

    public static void main(String[] args) {
        // 1,2,3,4,5
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next().toString();
        String[] arr = str.split(",");

        int[] ints = new int[arr.length];
        for (int j = 0; j < ints.length; j++) {
            ints[j] = Integer.parseInt(arr[j]);
        }

        ListNode head = InitListNode(ints);

        scanner.close();

        ListNode myhead = reverseList(head);

        // 输出
        // 1,5,2,4,3
        while (myhead != null) {
            if (myhead.next == null) {
                System.out.print(myhead.val);
            } else {
                System.out.print(myhead.val + ",");
            }
            myhead = myhead.next;
        }
    }
}

```

## **输入二叉树**

二叉树的数据结构

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```

```java

public static void main(String[] args) {
    TreeNode tn = InitTree(new Integer[]{1,2,3,4,null,2,4,null,null,4,null,null,null});
    List<TreeNode> res = findDuplicateSubtrees(tn);
}
public static TreeNode InitTree(Integer[] value) {
        TreeNode root = new TreeNode(value[0]);
        Queue<TreeNode> queue = new LinkedList<>();
        int current = 1;
        queue.offer(root);
        while (queue != null) {
            TreeNode node = queue.poll();

            // 左子树
            if (value[current] == null) {
                node.left=null;
            } else {
                node.left = new TreeNode(value[current]);
                queue.offer(node.left);
            }
            if (++current >= value.length) {
                break;
            }
            
            // 右子树
            if (value[current] == null) {
                node.right = null;
            } else {
                node.right = new TreeNode(value[current]);
                queue.offer(node.right);
            }
            if (++current >= value.length) {
                break;
            }
        }
        return root;
    }
```

下面这个是错的，有问题，但是还是可以看一下

```jsx
public static void main(String[] args) {
    TreeNode tn = convertArrToTree(new Integer[]{1,2,3,null,null,4,5});
    String res = serialize(tn);
}

public static TreeNode convertArrToTree(Integer[] nums) {
    TreeNode[] nodes = new TreeNode[nums.length];

    //创建每一层元素,创建好的节点放到数组里，方便
    for (int i = nums.length - 1; i >= 0; i--) {
        if (nums[i] == null) nodes[i] = null;
        else {
            nodes[i] = new TreeNode(nums[i]);

            //获取左右节点
            if (nums.length > (2 * i + 1)) {
                nodes[i].left = nodes[2 * i + 1];
            }
            if (nums.length > (2 * i + 2)) {
                nodes[i].right = nodes[2 * i + 2];
            }
        }
    }
    return nodes[0];
}
```

# 从上到下打印二叉树 层次遍历

```java
public static void PrintFromTopToBottom(TreeNode root) {
    ArrayList<Integer> list=new ArrayList<>();
    if(root == null){
        return;
    }
    Queue<TreeNode> q=new LinkedList<>();
    q.offer(root);
    while(!q.isEmpty()){
        TreeNode node=q.poll();
        list.add(node.val);
        if(node.left != null) q.offer(node.left);
        if(node.right != null) q.offer(node.right);
    }
    for(Integer i : list){
        System.out.print(i+" ");
    }
}
```