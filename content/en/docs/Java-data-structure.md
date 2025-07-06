---
title: Java Data Structure
slug: Java-Data-Structure
lastmod: 2025-07-01T00:00:00+00:00
---



import java.util.*;

# 基础类型相互转换

```java
// int & string
int a = Integer.parseInt(string);
int a = Integer.valueOf(str).intValue()

String string = String.valueOf(num)
String string = Integer.toString(num)

// int & char
int num = ch-'0'; //a 的 askii码是97
char ch = (char)(num + '0');

// string & char
String s = String.valueOf('c')
String s = Character.toString('c')

char ch = s.charAt(index)
char[] ch = s.toCharArray()
```

# Array

定义

```java
double[] myArray = new double[size];
int[] intArray = new int[] { 4, 1, 3, -23 };
```

使用Arrrays类进行查找和排序

```java
import java.util.Arrays

int[] nums = {2,5,0,4,6,-10};
Arrays.sort(nums);
Arrays.sort(nums, 0, 4);  //对前四位元素进行排序
Arrays.sort(nums, Collections.reverseOrder());
Arrays.sort(strs, String.CASE_INSENSITIVE_ORDER); //忽略大小写排序
Collections.reverse(Arrays.asList(strArray));

Arrays.fill(nums, 1);  //为数组元素填充相同的值
Arrays.fill(nums,2,5,3); //[2,5)填充3
Arrays.toString(nums);  //[2, 5, 0, 4, 1, -10]

Arrays.binarySearch(arr, 36);
```

# **ArrayList**

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素

```java
import java.util.ArrayList;
ArrayList<String> sites = new ArrayList<String>();
ArrayList<Character> li=new Arraylist<>();

sites.add(int index，E element) // 把元素插入到第几个位置
sites.add("Google");  // 如果 index 没有传入实际参数，元素将追加至数组的最末尾
sites.get(int index); // 访问第index+1个元素
sites.set(index, "Wiki"); // 第一个参数为索引位置，第二个为要修改的值
sites.remove(int index); // 删除第index+1个元素
sites.contains(Object obj) // 是否存在某个对象
sites.size();
String[] obj = sites.toArray();

// 遍历输出
for (String i : sites) {
    System.out.println(i);
}

for (Character i : li) {
    System.out.println(i);
}
```

Collections 类也是一个非常有用的类，位于 java.util 包中，提供的 sort() 方法可以对字符或数字列表进行排序

```java
ArrayList<String> sites = new ArrayList<String>();
Collections.sort(sites);  // 字母排序
```

# S**tack**

先进后出的原则

```java
Stack<Integer> st = new Stack<Integer>();
st.push(x);
int x = st.pop();
```

# **Queue**

队列是一种特殊的线性表，允许在表的前端进行删除操作，而在表的后端进行插入操作

LinkedList 类实现了 Queue 接口，因此我们可以把 LinkedList 当成 Queue 来用

```java
import java.util.LinkedList;
import java.util.Queue;

Queue<String> queue = new LinkedList<String>();
```

```java
queue.offer("a"); 
queue.poll();    //返回第一个元素，并在队列中删除
queue.element(); //返回第一个元素
queue.peek();    //返回第一个元素
queue.addAll(list);

Java 队列 queue的一些操作，
add        增加一个元索                     如果队列已满，则抛出一个IIIegaISlabEepeplian异常
remove   移除并返回队列头部的元素    如果队列为空，则抛出一个NoSuchElementException异常
element  返回队列头部的元素             如果队列为空，则抛出一个NoSuchElementException异常
offer       添加一个元素并返回true       如果队列已满，则返回false
poll         移除并返问队列头部的元素    如果队列为空，则返回null
peek       返回队列头部的元素             如果队列为空，则返回null
put         添加一个元素                      如果队列满，则阻塞
take        移除并返回队列头部的元素     如果队列为空，则阻塞
```

# Deque

```java
Deque deque = new LinkedList()
```

```java
addFirst(): 向队头插入元素，如果元素为空，则发生NPE(空指针异常)
addLast(): 向队尾插入元素，如果为空，则发生NPE
offerFirst(): 向队头插入元素，如果插入成功返回true，否则返回false
offerLast(): 向队尾插入元素，如果插入成功返回true，否则返回false
removeFirst(): 返回并移除队头元素，如果该元素是null，则发生NoSuchElementException
removeLast(): 返回并移除队尾元素，如果该元素是null，则发生NoSuchElementException
pollFirst(): 返回并移除队头元素，如果队列无元素，则返回null
pollLast(): 返回并移除队尾元素，如果队列无元素，则返回null
getFirst(): 获取队头元素但不移除，如果队列无元素，则发生NoSuchElementException
getLast(): 获取队尾元素但不移除，如果队列无元素，则发生NoSuchElementException
peekFirst(): 获取队头元素但不移除，如果队列无元素，则返回null
peekLast(): 获取队尾元素但不移除，如果队列无元素，则返回null
pop(): 弹出栈中元素，也就是返回并移除队头元素，等价于removeFirst()，如果队列无元素，则发生NoSuchElementException
push(): 向栈中压入元素，也就是向队头增加元素，等价于addFirst()，如果元素为null，则发生NPE，如果栈空间受到限制，则发生IllegalStateException
```

# PriorityQueue

优先队列 PriorityQueue 是 Queue 接口的实现，可以对其中元素进行排序

对于基本数据类型的包装器类，优先队列中元素默认排列顺序是升序排列。但对于自己定义的类来说，需要自己定义比较器

它为 add 和 poll 方法提供了 O(log(n)) 时间

```java
// 不用比较器，默认升序排列
Queue<Integer> q = new PriorityQueue<>();  // 小顶堆
// 用了比较器，可以降序排列
Queue<Integer> q = new PriorityQueue<>(cmp);
Queue<Integer> q = new PriorityQueue<>((x, y) -> (y - x));  // 大顶堆
Queue<Integer> q = new PriorityQueue<>((x, y) -> (x - y));  // 小顶堆
Queue<Integer> q = new PriorityQueue<>(Collections.reverseOrder());

//  小顶堆
PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>() {
    @Override
    public int compare(Integer a, Integer b) {
        return map.get(a) - map.get(b);
    }
});

q.peek()   //返回但不删除此队列的头部，如果此队列为空，则返回null
q.poll()   //返回并删除此队列的头部，如果此队列为空，则返回null
q.add(object)   // 将指定的元素插入此优先级队列
q.offer(object) // 将指定的元素插入此优先级队列
q.remove(object)// 从此队列中删除指定元素的单个实例
q.size()   
q.sEmpty()
q.contains(object)  // 如果此队列包含指定的元素，则返回true
```

排序比较器

```jsx
// 基本类型比较器
static Comparator<Integer> cmp = new Comparator<Integer>() {
      public int compare(Integer e1, Integer e2) {
        // 降序排列
        return e2 - e1;
        // 升序排列
        return e1 - e2;
      }
 };

```

```java

//类比较器
class Node{
        int chang;
      int kuan;
        public Node(int chang,int kuan){
                this.chang=chang;
                this.kuan=kuan;
        }
}

//自定义比较类，先比较长，长升序排列，若长相等再比较宽，宽降序
public class Test {
　　　　//自定义比较类，先比较长，长升序排列，若长相等再比较宽，宽降序
    static Comparator<Node> cmp=new Comparator<Node>() {
        public int compare(Node o1, Node o2) {
            if(o1.chang!=o2.chang)
                return o1.chang-o2.chang;
            else
                return o2.kuan-o1.kuan;
        }
        
    };
    public static void main(String[] args) {
        Queue<Node> q=new PriorityQueue<>(cmp);
        Node n1=new Node(1, 2);
        Node n2=new Node(2, 5);
        q.add(n1);
        q.add(n2);
        Node n;
        while(!q.isEmpty())
        {
            n=q.poll();
            System.out.println("长: "+n.chang+" 宽：" +n.kuan);
        }
}
```

记得如果要想按照排列好的顺序输出优先级的的话，用poll()的方法，而不是用迭代器迭代

PriorityQueue的 iterator() 不保证以任何特定顺序遍历队列元素。若想按特定顺序遍历，先将队列转成数组，然后排序遍历

```java
Queue<Integer> q = new PriorityQueue<>(cmp);
int[] nums= {2,5,3,4,1,6};
for(int i:nums)
{
  q.add(i);
}
Object[] nn=q.toArray();
Arrays.sort(nn);
for(int i=nn.length-1;i>=0;i--)
  System.out.print((int)nn[i]+" ");
```

# **String**

创建字符串

```clike
String str = "Runoob";
String str = new String("Runoob");

//通过char数组生成
char[] helloArray = { 'r', 'u', 'n', 'o', 'o', 'b'};
String helloString = new String(helloArray);
String helloString = new String(helloArray, 0, size);
String[] arr = str.split(",");
```

常用函数

```java
str.length();
str1.concat(str2);
str.charAt();
str.substring(0,i)
```

# **StringBuffer**

当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类

和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象

```java
StringBuilder sb = new StringBuilder(10);
sb.append("Runoob..");
sb.append("!");
sb.insert(8, "Java");we
sb.delete(5,8);
sb.deleteCharAt(sb.length()-1);
sb.toString();
sb.reverse();
```

# Set

# Map

java为数据结构中的映射定义了一个接口 java.util.Map

它有四个实现类，分别是 HashMap Hashtable LinkedHashMap TreeMap.

分别是HashMap Hashtable LinkedHashMap TreeMap

- Map主要用于存储健值对，根据键得到值，因此不允许键重复(重复了覆盖了),但允许值重复
- Hashmap 是一个最常用的Map,它根据键的HashCode值存储数据,根据键可以直接获取它的值，具有很快的访问速度，遍历时，取得数据的顺序是完全随机的。 HashMap最多只允许一条记录的键为Null;允许多条记录的值为 Null;HashMap不支持线程的同步
- Hashtable与 HashMap类似,它继承自Dictionary类，不同的是:它不允许记录的键或者值为空;它支持线程的同步，即任一时刻只有一个线程能写Hashtable,因此也导致了 Hashtable在写入时会比较慢
- LinkedHashMap 是HashMap的一个子类，保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的.也可以在构造时用带参数，按照应用次数排序。在遍历的时候会比HashMap慢
- TreeMap实现SortMap接口，能够把它保存的记录根据键排序,默认是按键值的升序排序，也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。

# H**ashMap**

HashMap 是一个散列表，它存储的内容是键值对(key-value)映射

HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 null，不支持线程同步

```java
import java.util.HashMap;

HashMap<Integer, String> Sites = new HashMap<Integer, String>();
Sites.put(1, "Google");     //添加键值对
Sites.put(3, "Taobao");
System.out.println(Sites); //打印hashmap，{1=Google}
Sites.get(3);       // Taobao
Sites.remove(3);    // 删除元素
Sites.clear();
Sites.size();
sites.getOrDefault(1, "Not Found");  //重要！要是查找第一个参数不到就返回第二个参数

//迭代 返回所有key和value的值
for (Integer i : Sites.keySet()) {
    System.out.println("key: " + i + " value: " + Sites.get(i));
}
for(String value: Sites.values()) {
    System.out.print(value + ", ");
}
```

[Untitled](Untitled%204b81e478566b4f0fa3f3086dd4bed47e.csv)

# LinkedHashMap

# Heap

堆是完全二叉树，找到子节点和父节点的方法

```java
public int left(int i) {
    return (i + 1) * 2 - 1;
}

public int right(int i) {
    return (i + 1) * 2;
}

public int parent(int i) {
    // i为根结点
    if (i == 0) {
        return -1;
    }
    return (i - 1) / 2;
}
```

顺堆

```java
public void heapify(T[] a, int i, int heapLength) {
    int l = left(i);
    int r = right(i);
    int largest = -1;
    /**
     * 下面两个if条件句用来找到三个元素中的最大元素的位置largest； 
     * l < heapLength说明l在数组内，i非叶子结点；
     */
    if (l < heapLength && a[i].compareTo(a[l]) < 0) {
        largest = l;
    } else {
        largest = i;
    }
    // r < heapLength说明r在数组内
    if (r < heapLength && a[largest].compareTo(a[r]) < 0) {
        largest = r;
    }
    // 如果i处元素不是最大的，就把i处的元素与最大处元素交换，交换会使元素下降
    if (i != largest) {
        T temp = a[i];
        a[i] = a[largest];
        a[largest] = temp;
        // 交换元素后，以a[i]为根的树可能不在满足大根堆性质，于是递归调用该方法
        heapify(a, largest, heapLength);
    }
}
```

建堆

```java
public  void buildHeap(T[] a, int heapLength) {
    // 从后往前看，lengthParent - 1处的元素是第一个有孩子节点的节点
    int lengthParent = parent(heapLength - 1);
    // 最初，parent(length)之后的所有元素都是叶子结点；
    // 因为大于length/2处元素的孩子节点如果存在，那么
    // 它们的数组下标值必定大于length，这与事实不符；
    // 在数组中，孩子元素必定在父亲元素的后面，从后往前
    // 对元素调用maxHeapify，保证了元素的孩子都是
    // 大根堆
    for(int i = lengthParent; i >= 0; i--){
        heapify(a, i, heapLength);
    }
}
```

# **ListNode**

```java
public class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
```

# **TreeNode 2**

二叉树 红黑树 索引树 b树 字典树 哈夫曼（压缩，可以用来加密解密）

看一下java的treenode接口一会

# **TreeNode N**

```java
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
```

# **TrieNode**

用于统计和排序大量的字符串，经常被搜索引擎系统用于文本词频统计

其核心思想是利用公共前缀来减少查询时间

```java
public class Trie2 {
    // 记录前缀树的根节点
    TreeNode root;
    // 定义前缀树节点
    class TreeNode{
        TreeNode[] next;
        boolean isEnd;
        public TreeNode (){
            next = new TreeNode[26];
        }
    }
    // 初始化前缀树
    public Trie2() {
        root = new TreeNode();
    }
    // 插入
    public void insert(String word) {
        TreeNode cur = root;
        for(char ch : word.toCharArray()){
            // 判断对应节点是否为空，如果为空，则直接插入
            if(cur.next[ch - 'a'] == null){
                cur.next[ch - 'a'] = new TreeNode();
            }
            // 继续插入下一个节点
            cur = cur.next[ch - 'a'];
        }
        // 将最后一个字符设置为结尾
        cur.isEnd = true;
    }

    // 查找单词
    public boolean search(String word) {
        TreeNode cur = root;
        for(char ch : word.toCharArray()){
            // 如果对应节点为空，则表明不存在这个单词，返回false
            if(cur.next[ch - 'a'] == null)
                return false;
            cur = cur.next[ch - 'a'];
        }
        // 检查最后一个字符是否是结尾
        return cur.isEnd;
    }

    // 查找前缀
    public boolean startsWith(String prefix) {
        TreeNode cur = root;
        for(char ch : prefix.toCharArray()){
            if(cur.next[ch - 'a'] == null)
                return false;
            cur = cur.next[ch - 'a'];
        }
        return true;
    }
```

# M**ath**

进制转换

```java
String st = Integer.toString(num, base); // 把num当做10进制的数转成base进制的st
int num = Integer.parseInt(st, base); // 把st当做base进制，转成10进制的int(parseInt有两个参数,第一个为要转的字符串,第二个为说明是什么进制).
BigInter m = new BigInteger(st, base); // st是字符串，base是st的进制.
```