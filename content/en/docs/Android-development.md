---
title: Andriod Development
slug: Andriod-Development
lastmod: 2025-07-01T00:00:00+00:00
---

[Android studio Windows 安装与配置](https://www.notion.so/Android-studio-Windows-bbd0a66c1ffa478fb3fbffa55b42d078?pvs=21)

[Android Studio Mac 安装与配置](https://www.notion.so/Android-Studio-Mac-d20410c14efb4bb68f6ff9834eefb97e?pvs=21)

## **一、开始启程**

### **1. 认识Android**

Android 大致可以分为4层架构：Linux内核层、系统运行库层、应用框架层和应用层

Android系统四大组件分别是Activity、Service、BroadcastReceiver和 ContentProvider

Android系统还自带了这种轻量级、运算速度极快的嵌入式关系型数据库， SQLite数据库，它不仅支持标准 的SQL语法，还可以通过Android封装好的API进行操作

### **2. 创建项目**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814140038.png)

**Package name**：表示项目的包名，Android系统就是通过包名来区分不同应用程序的，因此包名一定要具有唯一性

**Language**：这里默认选择了Kotlin。在过去，Android应用程序只能使用 Java来进行开发，本书的前两个版本也都是用Java语言讲解的。然而在2017年，Google引入 了一款新的开发语言——Kotlin，并在2019年正式向广大开发者公布了Kotlin First的消息

**Minimum API level**：设置项目的最低兼容版本，Android 5.0以 上的系统已经占据了超过85%的Android市场份额，因此这里我们将Minimum SDK指定成API 21就可以了

### **3. 分析第一个Android程序结构**

### **3.1 Project模式的项目结构**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814115516.png)

**.gradle和.idea**：放置的都是Android Studio自动生成的一些文件

**app**：项目中的代码、资源等内容都是放置在这个目录下的，我们后面的开发工作也基本是在这 个目录下进行的

**gradle**：这个目录下包含了gradle wrapper的配置文件，使用gradle wrapper的方式不需要提前将gradle下载好，而是会自动根据本地的缓存情况决定是否需要联网下载gradle。Android Studio默认就是启用gradle wrapper方式的，如果需要更改成离线模式，可以点击Android Studio导航栏→ File → Settings → Build, Execution, Deployment → Gradle，进行配置更改

**gitignore**：用来将指定的目录或文件排除在版本控制之外的

**build.gradle**：项目全局的gradle构建脚本

**gradle.properties**：全局的gradle配置文件

**gradlew和gradlew.bat**：用来在命令行界面中执行gradle命令的，其中gradlew是在Linux或Mac系统，gradlew.bat是在Windows系统

**local.properties**：指定本机中的Android SDK路径

**settings.gradle**：指定项目中所有引入的模块

### **3.2 app目录下的结构**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814135811.png)

**build**：包含了一些在编译时自动生成的文件

**libs**：放置第三方jar包

**androidTest**：编写测试用例

**java**：放置我们所有Java代码的地方（Kotlin代码也放在这里）

**res**：项目中使用到的所有图片、布局、字符串等资源

**AndroidManifest.xml**：是整个Android项目的配置文件，你在程序中定义的所有四大组件都需要在这个文件里注册

**test**：编写Unit Test测试用例

接下来分析一下HelloWorld项目究竟是**如何运行起来**的：

首先打开 AndroidManifest.xml，这段代码表示对MainActivity进行注册，intent-filter里的两行代码表示MainActivity是这个项目的主Activity

```
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

打开 MainActivity, 首先MainActivity是继承自AppCompatActivity (AndroidX中提供的一种向下兼容的Activity)，MainActivity中有一个onCreate()方法，里面调用了setContentView()方法，给当前的Activity引入了一个activity_main布局

```
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

打开 activity_main.xml，在 TextView中看到了“Hello World”的字样，因为Android程序的设计讲究逻辑和视图分离，不推荐在Activity中直接编写界面，而是在布局文件中编写界面

```
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### **3.3 res目录下的结构**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814141633.png)

以“drawable”开头的目录：用来放图片的

以“mipmap”开头的目录：用来放应用图标的

以“values”开头的目录：放字符串、样式、颜色等配置的

以“layout”开头的目录：放布局文件

我们应该如何使用这些资源呢，以字符串为例，这里定义了一个应用程序名的字符串，我们有以下两种方式来引用它

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814142244.png)

1. 在代码中通过R.string.app_name可以获得该字符串的引用。
2. 在XML中通过@string/app_name可以获得该字符串的引用

### **4. 一些error解决方法**

[ERROR: SSL peer shut down incorrectly错误解决(Android Studio)](https://www.cnblogs.com/rainbow70626/p/14337649.html)

错误信息：ERROR: SSL peer shut down incorrectly

错误原因：是studio工具不支持https请求

方法一：右上角 SDK Manager 进入到窗口里面 → 选择 SDK Update Sites 这个选项 → 勾选下方的 Force https// sources to be fetched using http// 选项 → 重启Android Studio → 点击右上大象图标重新下载

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814140533.png)

方法二：

将 gradle-wrapper.properties 文件里面的 distributionUrl=https 中的 https 改成 http，然后重新点击上方的按钮大象重新下载gradle文件

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814140710.png)

## **二、探究Activity**

Activity是一种可以包含用户界面的组件，主要用于和用户进行交互

### **1. 活动的基本用法**

### **1.1 创建活动**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814162359.png)

Generate Layout File：会自动创建一个对应的布局文件

Launcher Activity：会自动将这个Activity设置为当前项目的主Activity

项目中的任何Activity都应该重写onCreate()方法，调用setContentView()方法来给当前的Activity加载一个布局，我们一般会传入一个布局文件的id

```
public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
    }
}
```

### **1.2 Toast**

在程序中可以使用它将一些短小的信息通知给用户，一段时间后自动消失

在activity_main中添加一个button，并赋予id button_1

```
<Button
    android:id="@+id/button_1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="click"/>
```

在 onCreate() 方法中添加如下代码：

通过 findViewById() 获取在布局文件中定义的button_1，该方法返回的是一个继承自View的泛型对象，因此需要向下转型成Button对象

通过调用 setOnClickListener() 方法为按钮注册一个监听器，点击按钮时就会执行监听器中的 onClick() 方法，Toast的功能在  onClick() 方法中编写了

```
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    Button btn = (Button) findViewById(R.id.button_1);
    btn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Toast.makeText(MainActivity.this,"you clicked btn1",
                           Toast.LENGTH_SHORT).show();
        }
    });
}
```

Toast的用法：

通过静态方法 makeText() 创建出一个Toast对象，然后调用 show() 将Toast显示出来

第一个参数是Context，就是Toast要求的上下文，Activity本身就是一个Context对象，因此这里直接传入this。第二个参数是Toast显示的文本内容。第三个参数是Toast显示的时长，有两个内置常量可以选择：Toast.LENGTH_SHORT 和 Toast.LENGTH_LONG

### **1.3 Menu**

在res目录下新建一个menu文件夹，在menu文件夹下新建一个菜单文件 main.xml，代码如下，我们用 <item> 创建了两个菜单项

```
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/add_item"
        android:title="add"></item>
    <item
        android:id="@+id/remove_item"
        android:title="remove"></item>
</menu>
```

接着回到 MainActivity 来重写 onCreateOptionsMenu() 方法，getMenuInflater() 方法能够得到一 个MenuInflater 对象，再调用它的 inflate() 方法，就可以给当前Activity创建菜单了

inflate() 两个参数：第一个参数指定我们通过哪一个资源文件来创建菜单，第二个参数指定菜单项将添加到哪一个Menu对象当中，这里直接使用 onCreateOptionsMenu() 方法中传入的menu参数

返回 true，表示允许创建的菜单显示出来

```
@Override
public boolean onCreateOptionsMenu(Menu menu){
    getMenuInflater().inflate(R.menu.main,menu);
    return true;
}
```

我们继续给菜单定义响应事件

在 MainActivity中重写 onOptionsItemSelected() 方法，调用item.itemId来判断点击的是哪一个菜单项

```
@Override
public boolean onOptionsItemSelected(MenuItem item){
    switch (item.getItemId()) {
        case R.id.add_item:
            Toast.makeText(this, "You clicked Add",
                           Toast.LENGTH_SHORT).show();
            break;
        case R.id.remove_item:
            Toast.makeText(this, "You clicked Remove",
                           Toast.LENGTH_SHORT).show();
            break;
        default:
    }
    return true;
}
```

效果图如下

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814172231.png)

### **1.4 销毁一个活动**

按一下Back键，或者z在代码里使用 finish() 方法

```
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        finishi();
    }
});
```

### **2. Intent 在活动之间穿梭**

由一个Activity跳转到另一个Activity

### **2.1 Intent简介**

Intent是Android程序中各组件之间进行交互的一种方式，不仅可以指明当前组件想要执行的动作，还可以在不同组件之间传递数据，一般可用于启动Activity、启动Service以及发送广播等场景

### **2.2 显式Intent**

新建 SecondActivity.java 和 acitvity_second.xml，在布局文件里加上按钮id button_2

通过 Intent() 构造函数就可以构建出 Intent 对象的“意图”，第一个参数传入 MainActivity.this 作为上下文，第二个参数传入 SecondActivity.class 作为目标 Activity

Activity类中提供了一个 startActivity() 方法，接收一个Intent参数，专门用于启动Activity

```
Button btn = (Button) findViewById(R.id.button_1);
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        startActivity(intent);
    }
});
```

### **2.3 隐式Intent**

指定了一系列的action和category等信息，交由系统去分析这个Intent，找出合适的Activity去启动

打开 AndroidManifest.xml，通过在标签 <activity> 下配置 <intent-filter> 的内容，可以指定 SecondActivity 能够响应的 action 和 category

```
<activity android:name=".SecondActivity">
    <intent-filter>
        <action android:name="com.example.chapter2.ACTION_START" />
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</activity>
```

修改MainActivity中按钮的点击事件，只有 <action> 和 <category> 中的内容同时匹配Intent构造函数中指定的action和category时，这个Activity才能响应该Intent

```
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent("com.example.chapter2.ACTION_START");
        startActivity(intent);
    }
});
```

这里没有指定 category 是因为 DEFAULT 是一种默认的 category，调用函数时会自动添加进去

每个Intent中只能指定一个action，但能指定多个 category，在 MainActivity.java 里面调用 intent.addCategory()，再在SecondActivity的 <intent-filter>加上一个新的 <category>，否则会报错

```
Intent intent = new Intent(MainActivity.this,SecondActivity.class);
intent.addCategory("com.example.chapter2.MY_CATEGORY");
startActivity(intent);
```

```
<action android:name="com.example.chapter2.ACTION_START" />
<category android:name="com.example.chapter2.MY_CATEGORY"/>
<category android:name="android.intent.category.DEFAULT" />
```

### **2.4 更多隐式Intent的用法**

不仅可以启动自己程序内的Activity，还可以启动其他程序的Activity

- **Intent.ACTION_VIEW**
    
    首先指定了Intent的action是Intent.ACTION_VIEW，然后通过Uri.parse()方法将一个网址字符串解析成一个Uri对象，再调用Intent的 setData() 方法将这个Uri对象传递进去
    
    ```
    btn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent(Intent.ACTION_VIEW);
            intent.setData(Uri.parse("https://www.baidu.com"));
            startActivity(intent);
        }
    });
    ```
    
- **Intent.ACTION_DIAL**
    
    ```
    btn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent(Intent.ACTION_DIAL);
            intent.setData(Uri.parse("tel:10086"));
            startActivity(intent);
        }
    });
    ```
    
    点击按钮效果如图
    

### **2.5 向下一个activity传递数据**

Intent中提供了一系列 putExtra() 方法的重载，可以把我们想要传递的数据暂存在Intent中，在启动另一个Activity后，只需要把这些数据从Intent中取出就可以了

例如要把MainActivity中的字符串传递到SecondActivity中：

使用显式Intent的方式来启动SecondActivity，并通过 putExtra() 方法传递了一个字符串，第一个参数是键，用于之后从 Intent 中取值，第二个参数才是真正要传递的数据

```
btn1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        String data = "this is from MainActivity";
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        intent.putExtra("extra_data",data);
        startActivity(intent);
    }
});
```

在 SecondActivity中，调用父类的 getIntent() 方法，获取用于启动 SecondActivity的Intent，然后调用 getStringExtra() 方法传入相应的键值

传递字符串：getStringExtra()

传递整型数据：getIntExtra()

传递布尔值：getBooleanExtra()

```
public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);

        Intent intent = getIntent();
        String data = intent.getStringExtra("extra_data");
        Log.d("SecondActivity",data);
    }
}
```

### **2.6 返回数据给上一个活动**

Activity有一个用于启动Activity的 startActivityForResult() 方法，它期望在Activity销毁的时候能够返回一个结果给上一个Activity

**① 修改MainActivity代码**

用 startActivityForResult() 来启动活动，第一个参数还是Intent，第二个参数是请求码，用于在之后的回调中判断数据的来源

```
btn1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        startActivityForResult(intent,1);
    }
});
```

在 SecondActivity被销毁之后会回调上一个Activity的 onActivityResult() 方法，第一个参数是在启动 Activity 时传入的请求码，第二个参数是在返回数据时传入的处理结果；第三个参数即携带着返回数据的Intent

```
@Override
protected void onActivityResult(int rqCode, int resCode, Intent data) {
    switch (rqCode) {
        case 1:
            if(resCode == RESULT_OK) {
                String returnData = data.getStringExtra("data_return");
                Log.d("MainActivity",returnData);
            }
    }
}
```

**② 修改SecondActivity代码：**

构建一个Intent对象，仅用来传递数据，不指定任何意图

后调用了setResult()方法，专门用于向上一个Activity返回数据。第一个参数用于向上一个Activity返回处理结果（RESULT_OK 或 RESULT_CANCELED），第二个参数把带有数据的Intent传递回去

```
Button btn2 = (Button) findViewById(R.id.button_2);
btn2.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent();
        intent.putExtra("data_return","this is from SecondActivity");
        setResult(RESULT_OK,intent);
        finish();
    }
});
```

如果用户在SecondActivity中并不是通过点击按钮，而是通过按下Back键回到 FirstActivity，通过在SecondActivity中重写 onBackPressed() 方法来解决

```
@Override
public void onBackPressed(){
    Intent intent = new Intent();
    intent.putExtra("data_return","this is from SecondActivity");
    setResult(RESULT_OK,intent);
    finish();
}
```

### **3. 活动的生命周期**

### **3.1 返回栈**

Android中的Activity是可以层叠的，新活动覆盖在旧活动上

Android是使用任务（task）来管理Activity的，一个任务就是一组存放在栈里的Activity 的集合，这个栈称作返回栈（back stack）

### **3.2 Activity状态**

- 运行：位于返回栈的顶部，系统最不愿意回收
- 暂停：不在栈顶，但仍可见(例如对话框的背后)，暂停状态仍是完全存活的，系统不愿意回收
- 停止：不在栈顶，完全不可见，系统仍保为这个活动保存状态和成员变量，但在内存紧张会被回收
- 销毁：从返回栈移除，系统倾向回收，节约内存

### **3.3 Activity生存期**

完整生存期 ，onCreate —— onDestroy，初始化 —— 释放内存

可见生存期，onStart —— onStop，不可见 —— 可见时调用

前台展示生存期，onResume —— onPause

- onCreate，初始化，比如加载布局、绑定事件
- onStart，不可见到可见时调用
- onResume，和用户交互前进行调用，此时一定位于栈顶，处于运行状态
- onPause，在系统切换到另一个ACT时调用
- onStop，完全不可见时调用
- onDestroy，在销毁前被调用
- onRestart，从停止变为运行时调用，也就是Activity 被重新启动了

### **3.4 活动被回收了怎么办**

Activity被回收前，系统会调用一个方法onSaveInstanceState()来保存用户的数据，在 onPause 和onStop 之间，解决活动被回收临时数据得不到保留的问题

在 MainActivity 中写入函数

```
@Override
protected void onSaveInstanceState(Bundle outState){
    super.onSaveInstanceState(outState);
    String temp = "something you just typed";
    outState.putString("data_kay",temp);
}
```

我们一直使用的onCreate()方法也有一个Bundle参数，如果在Activity被系统回收之前，通过onSaveInstanceState()方法保存数据，这个参数就会带有之前保存的全部数据，只需要将数据取出即可

```
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    if(savedInstanceState != null){
        String temp = savedInstanceState.getString("data_key");
        log.d(TAG,temp);
    }
}
```

### **4. 活动的启动模式**

在实际项目中我们应该根据特定的需求为每个Activity指定恰当的启动模式，可以在AndroidManifest.xml中通过给标签指定 android:launchMode 属性来选择启动模式

- standard，默认的启动模式，每次创建都会产生一个新的，放在栈顶，不在乎以前是否创建过(单体可循环，默认情况)
- singleTop，每次创建时，如果发现栈顶是本身，就不再创建，否则就创建（交替可循环）
    
    ```
    android:launchMode="singleTop"
    ```
    
- singleTask，每次启动，系统首先会在返回栈中检查是否存在该Activity，如果已经存在则直接使用该实例， 并把在这个Activity之上的所有其他Activity统统出栈
- singleInstance，真正单态模式，自身拥有一个返回栈

## **三、UI开发的点滴**

### **1. 常用控件的使用方法**

### **1.1 TextView**

```
<TextView
          android:id="@+id/textView"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:gravity="center"
          android:text="This is TextView"/>
```

android:id  定义唯一标识符

android:text  文本内容

android:textColor  文字的颜色

android:textSize  文字的大小，文字大小使用sp作为单位

android:layout_width  控件的宽度

android:layout_height  控件的高度（match_parent、wrap_content、固定值，单位一般用dp）

android:gravity  文字的对齐方式（top、bottom、start、 end、center、center_vertical、center_horizontal）

### **1.2 Button**

```
<Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button" />
```

android:textAllCaps="false"  系统就会保留你指定的原始文字内容

在MainActivity中为Button的点击事件注册一个监听器

```
Button btn1 = (Button) findViewById(R.id.button_1);
btn1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        //在此处添加逻辑
    }
});
```

如果不喜欢匿名注册，也可以使用实现接口的方式来进行注册

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    Button btn1 = (Button) findViewById(R.id.button_1);
    btn1.setOnClickListener(this);
}

@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            //在此处添加逻辑
            break;
        default:
            break;
    }
}
```

### **1.3 EditText**

允许用户在控件里输入和编辑内容，并可以在程序中对这些内容进行处理

```
<EditText
          android:id="@+id/editText"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:hint="Type something here"
          android:maxLines="2"
          />
```

android:hint  指定一段提示性的文本

android:maxLines  指定了EditText的最大行数

通过点击按钮获取EditText中输入的内容：

调用EditText的 getText() 方法获取输入的内容，再调用toString() 方法将内容转换成字符串

```
private EditText editText;
private Button btn;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    editText = (EditText) findViewById(R.id.edit_Text);
    btn = (Button) findViewById(R.id.button_1);
    btn.setOnClickListener(this);
}

@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            String input = editText.getText().toString();
            Toast.makeText(MainActivity.this,input,Toast.LENGTH_SHORT).show();
            break;
        default:
            break;
    }
}
```

### **1.4 ImageView**

图片通常是放在以drawable开头的目录下，如果名称是纯数字会红色下划线报错

```
<ImageView
           android:id="@+id/img_view"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:src="@drawable/img1"
           />

```

宽和高都设定为wrap_content，保证了不管图片的尺寸是多少，都可以完整地展示出来

在按钮的点击事件里，可以动态地更改ImageView中的图片，通过调用ImageView的 ==setImageResource()== 方法将显示的图片改成 img2

```
private Button btn;
private ImageView img;
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    btn = (Button) findViewById(R.id.button_1);
    img = (ImageView) findViewById(R.id.img_view);
    btn.setOnClickListener(this);
}

@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            img.setImageResource(R.drawable.img2);
            break;
        default:
            break;
    }
}

```

### 1.5 ProgressBar

在界面上显示一个进度条，会看到屏幕中有一个圆形进度条正在旋转

```
<ProgressBar
             android:id="@+id/progressBar"
             android:layout_width="match_parent"
             android:layout_height="wrap_content"
             style="?android:attr/progressBarStyleHorizontal"
             android:max="100"
             />

```

**style**  可以将它指定成水平进度条或圆形进度条

**android:max**  给进度条设置一个最大值

**android:visibility**  可见属性，可选值有 visible、invisible、gone

**setVisibility()**  允许传入 View.VISIBLE、 View.INVISIBLE、View.GONE

**getVisibility()**  来判断ProgressBar是否可见

下面尝试实现一种效果：点击一下按钮让进度条消失，再点击一下按钮让进度条出现

```
private Button btn;
private ProgressBar prb;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    btn = (Button) findViewById(R.id.button_1);
    prb = (ProgressBar) findViewById(R.id.progress_bar);
    btn.setOnClickListener(this);
}

@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            if (prb.getVisibility() == View.GONE) {
                prb.setVisibility(View.VISIBLE);
            } else {
                prb.setVisibility(View.GONE);
            }
            break;
        default:
            break;
    }
}

```

尝试一种效果：给进度条设置一个最大值，然后在代码中动态地更改进度条的进度

```
@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            int prog = prb.getProgress();
            prog = prog + 10;
            prb.setProgress(prog);
            break;
        default:
            break;
    }
}

```

### 1.6 AlertDialog

在当前界面弹出一个对话框，重载 onClick() 函数

首先通过==AlertDialog.Builder==创建一个AlertDialog实例，为这个对话框设置标题、内容、可否使用Back键关闭对话框等属性

调用 ==setPositiveButton()== 设置确定按钮的点击事件，调用 ==setNegativeButton()== 设置取消按钮的点击事件，最后调用 ==show()== 方法将对话框显示出来

```
@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            AlertDialog.Builder dialog = new AlertDialog.Builder(MainActivity.this);
            dialog.setTitle("dialog title test");
            dialog.setMessage("dialog message test");
            dialog.setCancelable(false);

            dialog.setPositiveButton("YES", new DialogInterface.OnClickListener() {
                @Override
                public void onClick(DialogInterface dialogInterface, int i) {
                    //设置确定按钮点击事件
                }
            });
            dialog.setNegativeButton("NO", new DialogInterface.OnClickListener() {
                @Override
                public void onClick(DialogInterface dialogInterface, int i) {
                    //设置取消按钮点击事件
                }
            });
            dialog.show();
            break;
        default:
            break;
    }
}

```

效果如图：

![](https://img-blog.csdnimg.cn/img_convert/4ef027c7da64b7ac91bf22f147d7d666.png)

### 2. 详解3种基本布局

常用控件和布局的继承结构：

的所有控件都是直接或间接继承自View的，所用的所有布局都是直接或间接继承自ViewGroup的

![](https://img-blog.csdnimg.cn/img_convert/fa9c6cfe816958e5033a3edb5eea89a9.png)

### 2.1 LinearLayout

会将它所包含的控件在线性方向上依次排列

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
</LinearLayout>

```

**android:orientation**  垂直排列是vertical，水平排列是horizontal

**android:layout_gravity**  对齐方式，垂直方向（top、center_vertical、bottom）水平方向（left、right、center_horizontal）

**android:layout_weight**  来指定控件的大小，此时可以将宽度设定为0dp

注意：如果LinearLayout的排列方向是horizontal，控件宽度不能为match_parent，否则单独一个控件就会将整个水平方向占满，如果LinearLayout的排列方向是vertical，控件高度不能为为match_parent

注意：当LinearLayout的排列方向是horizontal时，只有垂直方向上的对齐方式才会生效，同理，是vertical时，只有 水平方向上的对齐方式才会生效

控件对齐方式举例：

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:orientation="horizontal"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <Button
            android:id="@+id/button1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="top"
            android:text="Button 1" />
    <Button
            android:id="@+id/button2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center_vertical"
            android:text="Button 2" />
    <Button
            android:id="@+id/button3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="bottom"
            android:text="Button 3" />
</LinearLayout>

```

以上按钮效果如图：

![](https://img-blog.csdnimg.cn/img_convert/891f0ae6b08c4dbf09da09769c20663d.png)

设置控件大小比重weight举例：

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:orientation="horizontal"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <EditText
              android:id="@+id/input_message"
              android:layout_width="0dp"
              android:layout_height="wrap_content"
              android:layout_weight="2"
              android:hint="Type something"
              />
    <Button
            android:id="@+id/send"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Send"
            />
</LinearLayout>

```

效果如图所示：

![](https://img-blog.csdnimg.cn/img_convert/5acd19ecee5dcd4247d0d8c92e280a9b.png)

### 2.2 RelativeLayout

相对布局，通过相对定位的方式让控件出现在布局的任何位置

```
<RelativeLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
                android:layout_width="match_parent"
                android:layout_height="match_parent">
    <Button
            android:id="@+id/button1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentLeft="true"
            android:layout_alignParentTop="true"
            android:text="Button 1" />
    <Button
            android:id="@+id/button2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentRight="true"
            android:layout_alignParentTop="true"
            android:text="Button 2" />
    <Button
            android:id="@+id/button3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:text="Button 3" />
    <Button
            android:id="@+id/button4"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentBottom="true"
            android:layout_alignParentLeft="true"
            android:text="Button 4" />
    <Button
            android:id="@+id/button5"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentBottom="true"
            android:layout_alignParentRight="true"
            android:text="Button 5" />
</RelativeLayout>

```

android:layout_alignParentLeft  父布局左对齐

android:layout_alignParentTop  父布局上对齐

android:layout_alignParentRight  父布局右对齐

android:layout_alignParentBottom  父布局下对齐

android:layout_centerInParent  父布局中心

以上五个按钮布局效果如下图：

![](https://img-blog.csdnimg.cn/img_convert/be423b72e368a8ce1534fbf37cfb59ba.png)

控件可以相对于父布局进行定位，也可以相对于控件进行定位

```
<RelativeLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
                android:layout_width="match_parent"
                android:layout_height="match_parent">
    <Button
            android:id="@+id/button3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:text="Button 3" />
    <Button
            android:id="@+id/button1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_above="@id/button3"
            android:layout_toLeftOf="@id/button3"
            android:text="Button 1" />
    <Button
            android:id="@+id/button2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_above="@id/button3"
            android:layout_toRightOf="@id/button3"
            android:text="Button 2" />
    <Button
            android:id="@+id/button4"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/button3"
            android:layout_toLeftOf="@id/button3"
            android:text="Button 4" />
    <Button
            android:id="@+id/button5"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/button3"
            android:layout_toRightOf="@id/button3"
            android:text="Button 5" />
</RelativeLayout>

```

android:layout_above  位于另一个控件的上方

android: layout_below 位于另一个控件的下方

android:layout_toLeftOf  位于另一个控件的左侧

android:layout_toRightOf  位于另一个控件的右侧

android:layout_alignLeft  左边缘和另一个控件的左边缘对齐

android:layout_alignRight  右边缘和另一个控件的右边缘对齐

android:layout_alignTop

android:layout_alignBottom

注意：当一个控件去引用另一个控件的id时，该控件一定要定义在引用控件的后面

![](https://img-blog.csdnimg.cn/img_convert/f196249feeac7994d88bcc9f1e0e0852.png)

### 2.3 FrameLayout

帧布局，所有的控件都会默认摆放在布局的左上角

```
<FrameLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
             android:layout_width="match_parent"
             android:layout_height="match_parent">
    <TextView
              android:id="@+id/textView"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="This is TextView"
              />
    <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"
            />
</FrameLayout>

```

可以看到，文字和按钮都位于布局的左上角，由于Button是在TextView之后添加的，因此按钮压在了文字的上面

![](https://img-blog.csdnimg.cn/img_convert/56f1c5d1f60e27cec555afc20ce811f3.png)

android:layout_gravity  对齐方式，和LinearLayout中的用法是相似的

### 3. 创建自定义组件

### 3.1 引入自定义布局

为了避免代码的大量重复，不用在每个Activity的布局中都编写一遍同样的代码

以实现一个标题栏自定义组件为例：

在layout目录下新建一个title.xml布局

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">
    <Button
        android:id="@+id/titleBack"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Back" />
    <TextView
        android:id="@+id/titleText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:gravity="center"
        android:text="Title Text"
        android:textSize="24sp" />
    <Button
        android:id="@+id/titleEdit"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Edit"/>
</LinearLayout>

```

android:background  为布局或控件指定一个背景

android:layout_margin  指定控件在上下左右方向上的间距

android:layout_marginLeft

android:layout_marginTop

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:layout_width="match_parent"
              android:layout_height="match_parent" >
              <include layout="@layout/title" />
</LinearLayout>

```

在程序中使用这个标题栏组件，就在activity_main.xml中加入 `<include layout="@layout/title" />`

最后别忘了在MainActivity中将系统自带的标题栏隐藏掉，调用了 ==getSupportActionBar()== 方法来获得ActionBar的实例，然后再调用它的hide()方法将标题栏隐藏起来

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ActionBar ab = getSupportActionBar();
    if(ab != null) {
        ab.hide();
    }
}

```

效果如图：

![](https://img-blog.csdnimg.cn/img_convert/32b0455c53c92fa96f0005111499a689.png)

### 3.2 创建自定义控件

是如果布局中有一些控件要求能够响应事件，我们还是需要在每个Activity中为这些控件单独编写一次事件注册的代码，这种情况使用自定义控件的方式来解决

新建==TitleLayout==继承自LinearLayout，成为我们自定义的标题栏控件

在TitleLayout的构造函数中声明了Context、AttributeSet这两个参数，在布局中引入TitleLayout控件时就会调用这个构造函数

通过==LayoutInflater==的==from()==方法可以构建出 一个LayoutInflater对象，然后调用==inflate()==方法就可以动态加载一个布局文件（第一个参数是要加载的布局文件的id，第二个参数是给加载好的布局再添加一个父布局）

```
public class TitleLayout extends LinearLayout {

    public TitleLayout(Context context, AttributeSet attrs) {
        super(context,attrs);
        LayoutInflater.from(context).inflate(R.layout.title,this);
    }
}

```

接下来我们需要在布局文件 activity_main.xml 中添加这个自定义控件，我们需要指明控件的完整类名，不可以省略

```
<com.example.chapter2.TitleLayout
     android:layout_width="match_parent"
     android:layout_height="wrap_content" />

```

下面我们为标题栏中的按钮注册点击事件

```
public TitleLayout(Context context, AttributeSet attrs) {
    super(context,attrs);
    LayoutInflater.from(context).inflate(R.layout.title,this);
    Button back = (Button) findViewById(R.id.titleBack);
    Button edit = (Button) findViewById(R.id.titleEdit);
    back.setOnClickListener(new OnClickListener() {
        @Override
        public void onClick(View view) {
            ((Activity)getContext()).finish();
        }
    });
    edit.setOnClickListener(new OnClickListener() {
        @Override
        public void onClick(View view) {
            Toast.makeText(getContext(),"you clicked edit button",Toast.LENGTH_SHORT).show();
        }
    });
}

```

这样的话，当我们在每一个布局中引入TitleLayout时，返回按钮和编辑按钮的点击事件就已经自动实现好了

### 4. listView 最常用的控件

ListView允许用户通过手指上下滑动的方式将屏幕外的数据滚动到屏幕内，同时屏幕上原有的数据会滚动出屏幕，比如查看QQ聊天记录，刷微博

### 4.1 ListView的简单用法

在 activity_main.xml 中加入 <ListView>

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
     android:layout_width="match_parent"
     android:layout_height="match_parent">
    <ListView
         android:id="@+id/listView"
         android:layout_width="match_parent"
         android:layout_height="match_parent" />
</LinearLayout>

```

这里简单使用一个字符串数组来模拟数据，但是数组中的数据无法直接传递给ListView，还需要借助适配器来完成

==ArrayAdapter==可以通过泛型来指定要适配的数据类型，然后在ArrayAdapter的构造函数中依次传入参数（Activity 的实例、ListView子项布局的id、数据源）

android.R.layout.==simple_list_item_1==，是一个 Android<u>内置的布局文件</u>，里面只有一个TextView，作为ListView子项布局的id

最后调用ListView的==setAdapter()==方法，将构建好的适配器对象传递进去

```
private String[] data = {"Apple", "Banana", "Orange", "Watermelon",
                         "Pear", "Grape", "Pineapple", "Strawberry", "Cherry",
                         "Mango","Apple", "Banana", "Orange", "Watermelon", "Pear",
                         "Grape","Pineapple", "Strawberry", "Cherry", "Mango"};

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    ArrayAdapter<String> adapter = new ArrayAdapter<String>(MainActivity.this, android.R.layout.simple_list_item_1,data);
    ListView lv = (ListView) findViewById(R.id.list_view);
    lv.setAdapter(adapter);
}

```

效果如图

![](https://img-blog.csdnimg.cn/img_convert/50605365ab232eda6c48a3f1ccf18cdb.png)

### 4.2 定制ListView页面

因为ListView实用性不强，用RecyclerView都能实现，所以此段先跳过，今后有时间再回来学

### 5. RecyclerView强大的滚动控件

RecyclerView，能够灵活的实现大数据集的展示，一个增强版的 ListView，能够显示列表、网格、瀑布流等形式，且不同的ViewHolder能够实现item多元化的功能

但是使用起来会稍微麻烦一点

### 5.1 基本用法

RecyclerView属于新增控件，我们需要在项目的build.gradle中添加RecyclerView库的依赖

打开app/build.gradle文件，在dependencies闭包中添加如下内容，如果你不能确定最新的版本号是多少，可以填入 1.0.0，当有更新的库版本时Android Studio会主动提醒你，填好之后点  sync now

```
implementation 'androidx.recyclerview:recyclerview:1.0.0'

```

修改 ==activity_main.xml==

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <androidx.recyclerview.widget.RecyclerView
              android:id="@+id/recyclerView"
              android:layout_width="match_parent"
              android:layout_height="match_parent" />
</LinearLayout>

```

新建==Fruit类==，作为适配器的适配类型

```
public class Fruit {
    private String name;
    private int imageid;
    public Fruit(String name,int imageid) {
        this.name = name;
        this.imageid = imageid;
    }

    public String getName() {
        return name;
    }

    public int getImageid() {
        return imageid;
    }
}

```

新建==fruit_item.xml==，指定自定义布局，注意布局的长和宽都要填 wrap_content

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content">

    <ImageView
        android:id="@+id/fruit_img"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
    <TextView
        android:id="@+id/fruit_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_vertical"
        android:layout_marginLeft="10dp"/>

</LinearLayout>

```

新建==FruitAdapter类==，为RecyclerView准备一个适配器，继承自 RecyclerView.Adapter，并将泛型指定为FruitAdapter.ViewHolder（ViewHolder是我们在FruitAdapter中定义的一个内部类）

1. 首先定义了一个内部类ViewHolder，主构造函数中传入RecyclerView子项的最外层布局，就可以通过findViewById()方法来获取布局中ImageView和TextView的实例
2. 接着，FruitAdapter中也有一个主构造函数，它用于把要展示的数据源传进来
3. 继续，由于FruitAdapter是继承自RecyclerView.Adapter的，那么就必须重写 ==onCreateViewHolder()、onBindViewHolder()、getItemCount()== 这3个方法
    - onCreateViewHolder()方法是用于创建ViewHolder实例
    - onBindViewHolder()方法用于对 RecyclerView 子项的数据进行赋值
    - getItemCount()方法用于告诉RecyclerView一共有多少子项

```
public class FruitAdapter extends RecyclerView.Adapter<FruitAdapter.ViewHolder> {
    private List<Fruit> mFruitList;

    static class ViewHolder extends RecyclerView.ViewHolder {
        ImageView fruitimg;
        TextView fruitname;
        public ViewHolder(View v) {
            super(v);
            fruitimg = (ImageView) v.findViewById(R.id.fruit_img);
            fruitname = (TextView) v.findViewById(R.id.fruit_name);
        }
    }

    public FruitAdapter(List<Fruit> fruitList) {
        mFruitList = fruitList;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent,int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.fruit_item,parent,false);
        ViewHolder holder = new ViewHolder(view);
        return holder;
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        Fruit fruit = mFruitList.get(position);
        holder.fruitimg.setImageResource(fruit.getImageid());
        holder.fruitname.setText(fruit.getName());
    }

    @Override
    public int getItemCount() {
        return mFruitList.size();
    }

}

```

修改MainActivity中的代码，开始使用RecyclerView

1. 使用了initFruits()方法，初始化所有的水果数据
2. 创建一个LinearLayoutManager对象，并将它设置到 RecyclerView当中，用于指定RecyclerView的布局方式，这里是线性布局的意思
3. 创建了FruitAdapter的实例，并将水果数据传入FruitAdapter的构造函数中
4. 调用 RecyclerView的setAdapter()方法来完成适配器设置

```
private List<Fruit> fruitList = new ArrayList<>();

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    initFruits();
    RecyclerView rv = (RecyclerView) findViewById(R.id.recycler_view);
    LinearLayoutManager llm = new LinearLayoutManager(this);
    rv.setLayoutManager(llm);
    FruitAdapter adp = new FruitAdapter(fruitList);
    rv.setAdapter(adp);

}

private void initFruits(){
    Fruit apple = new Fruit("Apple",R.drawable.apple_pic);
    fruitList.add(apple);
    Fruit banana = new Fruit("Banana",R.drawable.banana_pic);
    fruitList.add(banana);
    Fruit orange = new Fruit("Orange",R.drawable.orange_pic);
    fruitList.add(orange);
    Fruit cherry = new Fruit("Cherry",R.drawable.cherry_pic);
    fruitList.add(cherry);
    Fruit grape = new Fruit("Grape",R.drawable.grape_pic);
    fruitList.add(grape);
}

```

效果如图所示：

![](https://img-blog.csdnimg.cn/img_convert/096a7301a01aa8090310d7d3469511e2.png)

### 5.2 执行过程中遇到的问题

This project uses AndroidX dependencies, but the 'android.useAndroidX' property is not enabled.

解决方案：在gradle.properties里面加上一下代码

```
android.useAndroidX=true
android.enableJetifier=true

```

把每个activity前面的import android.support.v7.app.AppCompatActivity;改为

```
import androidx.appcompat.app.AppCompatActivity;

```

### 5.3 横向滚动

首先要对fruit_item布局进行修改，如果我们要实现横向滚动的话，应该把fruit_item里的元素改成垂直排列

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:orientation="vertical"
    android:layout_width="90dp"
    android:layout_height="wrap_content">

    <ImageView
        android:id="@+id/fruit_img"
        android:src="@drawable/apple_pic"
        android:layout_gravity="center_horizontal"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_margin="10dp"/>
    <TextView
        android:id="@+id/fruit_name"
        android:textSize="30dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_margin="10dp"/>

</LinearLayout>

```

接下来修改MainActivity中的代码：

只加入了一行代码，调用LinearLayoutManager的==setOrientation()==方法 设置布局的排列方向。默认是纵向排列的，我们传入==LinearLayoutManager.HORIZONTAL== 表示让布局横行排列

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    initFruits();
    RecyclerView rv = (RecyclerView) findViewById(R.id.recycler_view);
    LinearLayoutManager llm = new LinearLayoutManager(this);
    /* insert begin */
    llm.setOrientation(LinearLayoutManager.HORIZONTAL);
    /* insert end */
    rv.setLayoutManager(llm);
    FruitAdapter adp = new FruitAdapter(fruitList);
    rv.setAdapter(adp);
}

```

效果如图：

![](https://img-blog.csdnimg.cn/img_convert/8bad9a257034283a613b3400489b3b4f.png)

### 5.4 瀑布流布局

除了LinearLayoutManager之外，RecyclerView还给我们提供了另外两种内置的布局排列方式

- ==GridLayoutManager==：用于实现网格布局
- ==StaggeredGridLayoutManager==：用于实现瀑布流布局

首先修改一下fruit_item.xml中的代码，宽度改成match_parent

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_margin="5dp">>

    <ImageView
        android:id="@+id/fruit_img"
        android:layout_gravity="center_horizontal"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"/>
    <TextView
        android:id="@+id/fruit_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="10dp"/>

</LinearLayout>

```

接着修改MainActivity中的代码

1. 创建了一个==StaggeredGridLayoutManager==的实例，构造函数第一个参数用于指定布局的列数，传入3表示会把布局分为3列，第二个参数用于指定布局的排列方向，传入 StaggeredGridLayoutManager.VERTICAL表示纵向排列
2. 把创建好的实例设置到RecyclerView当中

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    initFruits();
    RecyclerView rv = (RecyclerView) findViewById(R.id.recycler_view);
    StaggeredGridLayoutManager sglm = new StaggeredGridLayoutManager(3,StaggeredGridLayoutManager.VERTICAL);

    rv.setLayoutManager(sglm);
    FruitAdapter adp = new FruitAdapter(fruitList);
    rv.setAdapter(adp);

}

```

可以把fruitname随机加长一些，以更好的看出瀑布流效果

```
private void initFruits(){
        for(int i=0;i<2;i++){
            Fruit apple = new Fruit(getRandomName("Apple"),R.drawable.apple_pic);
            fruitList.add(apple);
            Fruit banana = new Fruit(getRandomName("Banana"),R.drawable.banana_pic);
            fruitList.add(banana);
            Fruit orange = new Fruit(getRandomName("Orange"),R.drawable.orange_pic);
            fruitList.add(orange);
            Fruit cherry = new Fruit(getRandomName("Cherry"),R.drawable.cherry_pic);
            fruitList.add(cherry);
            Fruit grape = new Fruit(getRandomName("Grape"),R.drawable.grape_pic);
            fruitList.add(grape);
        }
    }

    private String getRandomName(String name) {
        Random rd = new Random();
        int length = rd.nextInt(20)+1;
        StringBuffer builder = new StringBuffer();
        for(int i = 0;i < length;i++）{
            builder.append(name);
        }
    }

```

效果如图：

![](https://img-blog.csdnimg.cn/img_convert/0c3533ce68ef90d50c887081dda3f092.png)

### 5.5 RecyclerView的点击事件

RecyclerView并没有提供类似于 setOnItemClickListener()这样的注册监听器方法，需要我们自己给子项具体的View 去注册点击事件

修改==FruitAdapter==中的代码

1. 在 ViewHolder 中添加fruitview来保存子项最外层布局的实例

```
static class ViewHolder extends RecyclerView.ViewHolder {
    View fruitview;
    ImageView fruitimg;
    TextView fruitname;
    public ViewHolder(View v) {
        super(v);
        fruitview = v;
        fruitimg = (ImageView) v.findViewById(R.id.fruit_img);
        fruitname = (TextView) v.findViewById(R.id.fruit_name);
    }
}

```

1. 在onCreateViewHolder()方法中注册点击事件，点击事件中先获取了用户点击的position，然后通过position拿到相应的Fruit实例

```
@Override
public ViewHolder onCreateViewHolder(ViewGroup parent,int viewType) {
    View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.fruit_item,parent,false);
    final ViewHolder holder = new ViewHolder(view);
    holder.fruitview.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            int position = holder.getAdapterPosition();
            Fruit fruit = mFruitList.get(position);
            Toast.makeText(view.getContext(),"you clicked"+fruit.getName(),Toast.LENGTH_SHORT).show();
        }
    });
    return holder;
}

```

尝试点击recyclerview弹出对话框，并删除该元素

```
@Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.log_item,parent,false);
        ViewHolder holder = new ViewHolder(view);
        holder.logview.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                int position = holder.getAdapterPosition();
                logData ld = mlogData.get(position);
                AlertDialog.Builder dialog = new AlertDialog.Builder(parent.getContext());
                dialog.setTitle("case intro");
                dialog.setMessage("you clicked"+ld.getTime()+ld.getTitle()+ld.getNeirong());
                dialog.setCancelable(false);

                dialog.setPositiveButton("delete", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        mlogData.remove(ld);
                        notifyItemRemoved(mlogData.size());
                        //notifyItemRangeChanged(mlogData.size());
                    }
                });
                dialog.setNegativeButton("back", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        //设置取消按钮点击事件
                    }
                });
                dialog.show();
            }
        });
        return holder;
    }

```

## 三、探究Fragment

为了兼顾手机和平板的开发

Fragment是一种可以嵌入在Activity当中的UI片段，它能让程序更加合理和充分地利用大屏幕的空间

可以理解成一个迷你型的Activity

![](https://img-blog.csdnimg.cn/img_convert/722785c8b50cfb5e732888dfbb21d734.png)

![](https://img-blog.csdnimg.cn/img_convert/516409b53b04903062f0c5db01f69b3e.png)

### 1. Fragment的使用方式

创建一个平板模拟器pixel C

![](https://img-blog.csdnimg.cn/img_convert/0aee00d1ddc0a22df209a2653839c85d.png)

下面我们尝试在一个Activity当中添加两个 Fragment，并让这两个Fragment平分Activity的空间

新建一个左侧Fragment的布局left_fragment.xml

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:orientation="vertical"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal"
            android:text="Button"
            />
</LinearLayout>

```

新建右侧Fragment的布局right_fragment.xml

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:orientation="vertical"
              android:background="#00ff00"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <TextView
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:layout_gravity="center_horizontal"
              android:textSize="24sp"
              android:text="This is right fragment"
              />
</LinearLayout>

```

新建一个LeftFragment类，并让它继承自Fragment，请一定要使用AndroidX库中的Fragment，使用AndroidX库中的Fragment并不需要在build.gradle文件中添加额外的依赖

是重写了Fragment的onCreateView()方法，然后在这个方法中通过 LayoutInflater的inflate()方法将刚才定义的left_fragment布局动态加载进来

```
public class LeftFragment extends Fragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState){
        View v = inflater.inflate(R.layout.left_frag,container,false);
        return v;
    }
}

```

用同样的方法再新建一个RightFragment

```
public class RightFragment extends Fragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState){
        View v = inflater.inflate(R.layout.right_frag,container,false);
        return v;
    }
}

```

接下来修改activity_main.xml中的代码，我们使用了标签在布局中添加Fragment，过这里还需要通过android:name属性来显式声明要添加的Fragment类名，注意一定要将类的包名也加上

```
<fragment
          android:id="@+id/leftFrag"
          android:name="com.example.fragmenttest.LeftFragment"
          android:layout_width="0dp"
          android:layout_height="match_parent"
          android:layout_weight="1" />
<fragment
          android:id="@+id/rightFrag"
          android:name="com.example.fragmenttest.RightFragment"
          android:layout_width="0dp"
          android:layout_height="match_parent"
          android:layout_weight="1" />

```

结果如图：

![](https://img-blog.csdnimg.cn/img_convert/cae71221dda59136b76897a74cddf5ab.png)

### 2. 动态添加Fragment

可以在程序运行时动态地添加到Activity当中

新建another_right_fragment.xml

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:orientation="vertical"
              android:background="#ffff00"
              android:layout_width="match_parent"
              android:layout_height="match_parent">
    <TextView
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:layout_gravity="center_horizontal"
              android:textSize="24sp"
              android:text="This is another right fragment"
              />
</LinearLayout>

```

然后新建AnotherRightFragment作为另一个右侧Fragment

```
public class AnotherRightFragment extends Fragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState){
        View v = inflater.inflate(R.layout.another_right_frag,container,false);
        return v;
    }
}

```

接下来看一下如何将它动态地添加到Activity当中，修改activity_main.xml，在将右侧==Fragment替换成了一个FrameLayout==

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:orientation="horizontal"
              android:layout_width="match_parent"
              android:layout_height="match_parent" >
    <fragment
              android:id="@+id/leftFrag"
              android:name="com.example.fragmenttest.LeftFragment"
              android:layout_width="0dp"
              android:layout_height="match_parent"
              android:layout_weight="1" />
    <FrameLayout
                 android:id="@+id/rightLayout"
                 android:layout_width="0dp"
                 android:layout_height="match_parent"
                 android:layout_weight="1" >
    </FrameLayout>
</LinearLayout>

```

修改 MainActivity中的代码，在代码中向FrameLayout里添加内容，从而实现动态添加Fragment的功能

1. 创建待添加Fragment的实例
2. 获取FragmentManager，在Activity中可以直接调用==getSupportFragmentManager()== 方法获取
3. 开启一个事务，通过调用==beginTransaction()==方法开启
4. 向容器内添加或替换Fragment，一般使用==replace()==方法实现，需要传入容器的id和待添 加的Fragment实例
5. 提交事务，调用commit()方法来完成

```
public class FragmentActivity extends AppCompatActivity implements View.OnClickListener{

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_fragment);

        Button left_btn = (Button) findViewById(R.id.left_button);
        left_btn.setOnClickListener(this);
        replaceFragment(new RightFragment());

    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.left_button:
                replaceFragment(new AnotherRightFragment());
                break;
            default:
                break;
        }
    }

    private void replaceFragment(Fragment frag) {
        FragmentManager fm = getSupportFragmentManager();
        FragmentTransaction ft = fm.beginTransaction();
        ft.replace(R.id.rightLayout,frag);
        ft.commit();
    }
}

```

效果如下：我们点击一下左侧的按钮，右边的板块就会从绿色变成黄色

![](https://img-blog.csdnimg.cn/img_convert/469170f3e1e6e955f6d9da165af4e9f9.png)

### 3. 在Fragment中实现返回栈

按下Back键可以回到上一个Fragment，而不是直接退出程序

修改MainActivity中的代码，在事务提交之前调用了FragmentTransaction的==addToBackStack()==方法

```
private void replaceFragment(Fragment frag) {
    FragmentManager fm = getSupportFragmentManager();
    FragmentTransaction ft = fm.beginTransaction();
    ft.replace(R.id.rightLayout,frag);
    ft.addToBackStack(null);
    ft.commit();
}

```

Back，程序回到了RightFragment界面

继续 Back，RightFragment界面也会消失

再次 Back，程序才会退出

### 4. Fragment和Activity之间的交互

Fragment和Activity是各自存在于一个独立的类当中的，它们之间并没有那么明显的方式来直接进行交互

- **活动调用碎片：**
    
    FragmentManager提供了一个类似于 findViewById()的方法，专门用于从布局文件中获取Fragment的实例
    
    ```
    RightFragment rf = (RightFragment) getFragmentManager().findFragmentById(R.id.rightLayout);
    
    ```
    
- **碎片调用活动**
    
    通过调用==getActivity()==方法来得到 和当前Fragment相关联的Activity实例，当Fragment 中需要使用Context对象时，也可以使用getActivity()方法
    
    ```
    MainActivity act = (MainActivity) getActivity();
    
    ```
    

### 5. Fragment的生命周期

### 5.1 Fragment的状态

运行状态：所关联的Activity正处于运行状态时

暂停状态：当一个Activity进入暂停状态时

停止状态：当一个Activity进入停止状态时，是完全不可见的

销毁状态：Fragment总是依附于Activity而存在，因此当Activity被销毁时，与它相关联的 Fragment 就会进入销毁状态

### 5.2 Fragment的回调方法

Fragment提供了一些附加的回调方法：

- onAttach()：当Fragment和Activity建立关联时调用
- onCreateView()：为Fragment创建视图（加载布局）时调用
- onActivityCreated()：确保与Fragment相关联的Activity已经创建完毕时调用
- onDestroyView()：当与Fragment关联的视图被移除时调用
- onDetach()：当Fragment和Activity解除关联时调用

![](https://img-blog.csdnimg.cn/img_convert/1f65dd4aea9b50ec6088ccd0db7f9658.png)

## 五、详解广播机制

Android中的每个应用程序都可以对自己感兴趣的广播进行注册，这样该程序就只会收到自己所关心的广播内容，这些广播可能是来自于系统的，也可能是来自于其他应用程序的

Android提供了一套完整的API，允许应用程序自由地发送和接收广播

Android中的广播主要可以分为两种类型：==标准广播和有序广播==

- **标准广播**
    
    完全异步执行，所有的 BroadcastReceive r几乎会在同一时刻收到这条广播消息，因此它们之间没有任何先后顺序可言
    
    ![](https://img-blog.csdnimg.cn/img_convert/9d6b463558ff37a3ff1a6e1af7389c57.png)
    
- **有序广播**
    
    同步执行，同一时刻只会有一个BroadcastReceiver能够收到这条广播消息，当这个BroadcastReceiver中的逻辑执行完毕后，广播才会继续传递，有先后顺序的
    
    ![](https://img-blog.csdnimg.cn/img_convert/73006bb41cadb01e86d07cc64915734c.png)
    

### 1. 接受系统广播

我们可以在应用程序中通过监听这些广播来得到各种系统的状态信息，比如手机开机完成、亮屏熄屏、网络变化、电池电量变化、系统时间改变都会发出一条广播

### 1.1 动态注册监听时间变化

注册 BroadcastReceiver 的方式一般有两种：在代码中注册和在AndroidManifest.xml中注册。其中前者也被称为==动态注册==，后者也被称为==静态注册==

**下面尝试实现监听系统网络变化的广播：**

修改BroadcastActivity中的代码

1. 定义了一个内部类 ==NetworkChangeReceiver==，这个类是继承 自BroadcastReceiver的，并重写了父类的onReceive()方法
2. 创建了一个==IntentFilter==的实例，并给它添加了一个值为android.net.cnn.CONNECTIVITY_CHANGE 的action，因为当系统网络发生变化时，系统发出的正是一条值为android.net.cnn.CONNECTIVITY_CHANGE的广播
3. 接下来创建一个==NetworkChangeReceiver==的实例，然后调用==registerReceiver()==方法进行注册，这样 TimeChangeReceiver 就会收到所有值为android.net.cnn.CONNECTIVITY_CHANGE 的广播
4. 最后，动态注册的BroadcastReceiver一定要取消注册才行，通过调用==unregisterReceiver()==方法

```
public class BroadcastActivity extends AppCompatActivity {

    private IntentFilter inf;
    private NetworkChangeReceiver ncr;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_broadcast);

        inf = new IntentFilter();
        inf.addAction("android.net.cnn.CONNECTIVITY_CHANGE");
        ncr = new NetworkChangeReceiver();
        registerReceiver(ncr,inf);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(ncr);
    }

    class NetworkChangeReceiver extends BroadcastReceiver {
        @Override
        public void onReceive(Context context, Intent intent) {
            Toast.makeText(context,"network changes",Toast.LENGTH_SHORT).show();
        }
    }
}

```

对上面代码进一步优化，能够准确的告诉用户当前是什么网络状态

```
class NetworkChangeReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        ConnectivityManager cm = (ConnectivityManager) getSystemService(Context.CONNECTIVITY_SERVICE);
        NetworkInfo ni = cm.getActiveNetworkInfo();
        if(ni!=null && ni.isAvailable()) {
            Toast.makeText(context,"network is available",Toast.LENGTH_SHORT).show();
        } else {
            Toast.makeText(context,"network is unavailable",Toast.LENGTH_SHORT).show();
        }
    }
}

```

另外，安卓为了保护用户设备的安全隐私，如果程序进行一些对用户来说比较敏感的操作，就必须在配置文件中声明权限，比如这里的访问网络

```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

```

### 1.2 静态注册实现开机启动

让程序在未启动的情况下也能接收广播

这里我们准备实现一个开机启动的功能，在开机的时候我们的应用程序肯定是没有启动， 因此显然不能使用动态注册的方式来实现，而应该使用静态注册的方式来接收开机广播

右击 →New→Other→Broadcast Receiver，创建的类命名为BootCompleteReceiver，Exported属性允许这个BroadcastReceiver接收本程序以外的广播，Enabled属性表示启用这个 BroadcastReceiver，勾选这两个属性

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-UBGXXq9s-1629976477557)(C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210819145835685.png)]

```
public class BootCompleteReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        // TODO: This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        Toast.makeText(context,"boot complete",Toast.LENGTH_SHORT).show();
    }
}

```

另外，静态的BroadcastReceiver一定要在AndroidManifest.xml文件中注册

```
<application>
<receiver
          android:name=".BootCompleteReceiver"
          android:enabled="true"
          android:exported="true"></receiver>
</application>

```

我们还需要对 AndroidManifest.xml文件进行修改

由于Android系统启动完成后会发出一条值为==android.intent.action.BOOT_COMPLETED== 的广播，因此我们在标签中又添加了一个标签，并在里面声明了相应的action

```
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
<application>
    <receiver
              android:name=".BootCompleteReceiver"
              android:enabled="true"
              android:exported="true">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED"/>
        </intent-filter>
    </receiver>
</application>

```

### 2. 发送自定义广播

### 2.1 发送标准广播

要先定义一个静态BroadcastReceiver来准备接收此广播，以上方法自动生成一个MyBroadcastReceiver，并重写onReceive()方法

```
public class MyBroadcastReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        // TODO: This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        Toast.makeText(context,"received in MyBroadcastReceiver",Toast.LENGTH_LONG).show();
    }
}

```

然后在AndroidManifest.xml中对这个BroadcastReceiver进行修改，指定action，这里让MyBroadcastReceiver接收一条值为 ==com.example.chapter3.MY_BROADCAST==的广播

```
<receiver
          android:name=".MyBroadcastReceiver"
          android:enabled="true"
          android:exported="true">
    <intent-filter>
        <action android:name="com.example.chapter3.MY_BROADCAST"/>
    </intent-filter>
</receiver>

```

接下来修改activity_main.xml中的代码，定义了一个按钮，用于作为发送广播的触发点

```
<Button
        android:id="@+id/btn_send"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Send Broadcast"
        />

```

然后修改MainActivity中的代码，在按钮的点击事件里面加入了发送自定义广播的逻辑

1. 构建了一个Intent对象，并把要发送的广播的值传入
2. 调用==sendBroadcast()==方法将广播发送出去，这样所有监听com.example.broadcasttest.MY_BROADCAST这条广播的BroadcastReceiver就会收到消息了

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_send_broadcast);

    Button send = (Button) findViewById(R.id.btn_send);
    send.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent("com.example.chapter3.MY_BROADCAST");
            sendBroadcast(intent);
        }
    });
}

```

注意，因为安卓高版本对隐式广播进行了限制，因而用setComponent()才能接收到广播，参数一是你的包名，参数二是你的接收器

```
Intent intent = new Intent();
intent.setComponent(new ComponentName("com.example.myapplication","com.example.myapplication.MyBroadcastReceiver" ));
sendBroadcast(intent); //发送广播

```

### 2.2 发送有序广播

新建项目BroadcastTest2，新建AnotherBroadcastReceiver，依然用来接收广播

```
public class AnotherBroadcastReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        // TODO: This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        Toast.makeText(context,"received in AnotherBroadcastReceiver",Toast.LENGTH_LONG).show();
    }
}

```

在BroadcastTest2的AndroidManifest.xml中对这个BroadcastReceiver的配置进行修改

AnotherBroadcastReceiver同样接收的是 com.example.broadcasttest.MY_BROADCAST这条广播，重新运行程序，并点击“Send Broadcast”，就会分别弹出两次提示信息，==说明应用程序发出的广播是可以被其他应用程序接受到的==

```
<receiver
          android:name=".AnotherBroadcastReceiver"
          android:enabled="true"
          android:exported="true">
    <intent-filter>
        <action android:name="com.example.chapter3.MY_BROADCAST" />
    </intent-filter>
</receiver>

```

![](https://img-blog.csdnimg.cn/img_convert/fdf256bc248b377a35f460dd07ce4b3a.png)

不过到目前为止，程序发出的都是**标准广播**，现在来尝试一下发送**有序广播**

修改MainActivity中的代码，将sendBroadcast()方法改成 sendOrderedBroadcast()方法

```
sendOrderedBroadcast(intent,null);

```

重新运行程序并点击“Send Broadcast”，两个BroadcastReceiver仍然都可以收到这条广播

下面尝试在注册的时候设定BroadcastReceiver的**先后顺序**呢，修改 AndroidManifest.xml，通过==android:priority==属性设置了优先级，优先级高的先收到广播

```
<receiver
          android:name=".MyBroadcastReceiver"
          android:enabled="true"
          android:exported="true">
    <intent-filter android:priority="100">
        <action android:name="com.example.chapter3.MY_BROADCAST" />
    </intent-filter>
</receiver>

```

如果在onReceive()方法中调用了==abortBroadcast()==方法，就表示将这条广播截断，后面的将无法再接收到这条广播

```
public class MyBroadcastReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        // TODO: This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        Toast.makeText(context,"received in MyBroadcastReceiver",Toast.LENGTH_LONG).show();
        abortBroadcast();
    }
}

```

### 3. 实践：实现强制下线功能

## 六、数据存储

保存在内存中的数据是处于瞬时状态的，而保存在存储设备中的数据是处于持久状态的。

持久化技术提供了一种机制，可以让数据在瞬时状态和持久状态之间进行转换

### 1. 文件存储

不对存储的内容进行任何格式化处理，所有数据都是原封不动地保存到文件当中

### 1.1 将数据存储到文件中

Context类中提供了一个==openFileOutput()==方法，可以用于将数据存储到指定的文件中，第一个参数是文件名，在文件创建的时候使用，第二个参数是文件的操作模式，主要有MODE_PRIVATE和MODE_APPEND两种模式

在布局中加入了一个EditText，用于输入文本内容

```
<EditText
          android:id="@+id/edit"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"/>

```

修改MainActivity中的代码，在数据被回收之前，将它存储到文件当中

1. 构造==save()==函数，通过openFileOutput()方法能够得到一个==FileOutputStream对象==，然后借助它构建出一个==OutputStreamWriter对 象==，接着再使用OutputStreamWriter构建出一个==BufferedWriter对象==，这样你就可以通过BufferedWriter将文本内容写入文件中
2. 重写了onDestroy()方法，获取了EditText中输入的内容，并调用save()

```
public class FileStorageActivity extends AppCompatActivity {

    private EditText edit;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_file_storage);
        edit = (EditText) findViewById(R.id.edit);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        String input = edit.getText().toString();
        save();
    }

    public void save(String input) {
        FileOutputStream out = null;
        BufferedWriter writer = null;
        try {
            out = openFileOutput("data", Context.MODE_PRIVATE);
            writer = new BufferedWriter(new OutputStreamWriter(out));
            writer.write(input);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if(writer != null) {
                    writer.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```

证明数据确实已经保存成功：在输入框输入数据之后返回前一个活动 —> Device File Explorer —> /data/data/com.example.chapter6/files/ 目录 —> 已经生成了一个data文件

![](https://img-blog.csdnimg.cn/img_convert/56e17ec656a48bc1c495677f85a73a08.png)

![](https://img-blog.csdnimg.cn/img_convert/a188e3c084c60e07e11b72179f797a8f.png)

### 1.2 从文件中读取数据

Context类中还提供了一个==openFileInput()==方法，用于从文件中读取数据，系统会自动到/data/data//files/目录下加载这个文件，并返回一个FileInputStream对象

在main_activity里加入load()函数：

1. 通过openFileInput()方法获取了一个==FileInputStream==对象
2. 借助它构建出一个==InputStreamReader==对象
3. 再使用InputStreamReader构建出 一个==BufferedReader==对象，这样我们就可以通过BufferedReader将文件中的数据一行行读取出来，并拼接到==StringBuilder对象==

```
public String load() {
    FileInputStream in = null;
    BufferedReader reader = null;
    StringBuffer content = new StringBuffer();
    try {
        in = openFileInput("data");
        reader = new BufferedReader(new InputStreamReader(in));
        String line = "";
        while ((line = reader.readLine())!=null) {
            content.append(line);
        }

    }catch(IOException e) {
        e.printStackTrace();
    }finally {
        if(reader != null) {
            try {
                reader.close();
            }catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    return content.toString();
}

```

修改onCreate()代码：

1. 调用load()方法读取文件
2. 如果读到内容非空，就调用EditText的==setText()方法==将内容填充，并调用==setSelection()方法==将输入光标移动到文本的末尾位置

```
public class FileStorageActivity extends AppCompatActivity {

    private EditText edit;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_file_storage);
        edit = (EditText) findViewById(R.id.edit);

        /***insert begin***/
        String input = load();
        if(!TextUtils.isEmpty(input)){
            edit.setText(input);
            edit.setSelection(input.length());
            Toast.makeText(this,"restoring succeeded",Toast.LENGTH_LONG).show();
        }
        /***insert end***/
    }

    @Override
    protected void onDestroy() {
        ......
    }

    public void save(String input) {
        ......
    }

    public String load() {
        ......
    }
}

```

现在重新启动程序时EditText中能够保留我们上次输入的内容

![](https://img-blog.csdnimg.cn/img_convert/7174b08f9488b094f72cc3a2f2458a84.png)

### 2. SharedPreferences存储

使用键值对的方式来存储数据

支持多种不同的数据类型存储

### 2.1 将数据存储到SharedPreferences中

Android中主要提供了以下两种方法用于==得到SharedPreferences对象==：

- Context类中的getSharedPreferences()方法，第一个参数用于指定SharedPreferences文件的名称，第二个参数用于指定操作模式
- Activity类中的getPreferences()方法，只接收一个操作模式参数

得到了SharedPreferences对象之后，就可以开始==向SharedPreferences文件中存储数据==了，主要：

- 调用SharedPreferences对象的edit()方法获取一个 SharedPreferences.Editor对象
- 向SharedPreferences.Editor对象中添加数据，比如添加一个字符串则使用putString()方法，以此类推
- 调用apply()方法将添加的数据提交

现在开始：

先在avtivity_main.xml中添加一个存储数据按钮

```
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical" >
    <Button
            android:id="@+id/saveButton"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Save Data"
            />
</LinearLayout>

```

给按钮注册点击事件，通过 ==getSharedPreferences()==方法指定文件名为data，并得到了 SharedPreferences.Editor 对象

```
Button savaData = (Button) findViewById(R.id.saveButton);
savaData.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        SharedPreferences.Editor editor = getSharedPreferences("data",MODE_PRIVATE).edit();
        editor.putString("name","Tom");
        editor.putInt("age",18);
        editor.putBoolean("married",false);
        editor.apply();
    }
});

```

运行一下程序了，点击一下“Save Data”按钮。这时的数据应该已经保存成功了

### 2.2 从SharedPreferences中读取数据

SharedPreferences对象中提供了一系列的get方法，用于读取存储的数据

先在avtivity_main.xml中添加一个读取数据按钮

```
<Button
        android:id="@+id/restoreButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Restore Data"
        />

```

给按钮注册点击事件，来从SharedPreferences文件中读取数据

首先通过==getSharedPreferences()==方法得到 了SharedPreferences对象，然后分别调用它的getString()、getInt()和 getBoolean()方法

```
Button restoreData = (Button) findViewById(R.id.restoreButton);
restoreData.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        SharedPreferences pref = getSharedPreferences("data",MODE_PRIVATE);
        String name = pref.getString("name","");
        int age = pref.getInt("age",0);
        boolean married = pref.getBoolean("married",false);
        Log.d("MainActivity",name);
        Log.d("MainActivity",name);
        Log.d("MainActivity",name);
    }
});

```

### 3. SQLite数据库存储

文件存储和SharedPreferences存储只适用于保存一些简单的数据和键值对，当需要存储大量复杂的关系型数据的时候，Android系统竟然是内置了数据库的

### 3.1 创建数据库

借助==SQLiteOpenHelper帮助类==：

SQLiteOpenHelper是一个抽象类，我们想要使用它就需要创建一个自己的帮助类去继承它，必须在自己的帮助类里重写onCreate()和 onUpgrade() 这两个方法，分别在这两个方法中实现创建和升级数据库的逻辑

数据库文件会存放在/data/data//databases/目录下

内置方法：

- getReadableDatabase()
- getWritableDatabase()

**下面开始具体的例子：**

新建MyDatabaseHelper类继 承自SQLiteOpenHelper

1. 把SQL语句放在CREATE_BOOK字符串里面，integer表示整型，real表示浮点型，text表示文本类型，blob表示二进制类型
2. 在onCreate()方法中又调用了 SQLiteDatabase的==execSQL()==方法去执行这条建表语句

```
public class MyDataBaseHelper extends SQLiteOpenHelper {

    public static final String CREATE_BOOK = "create table Book("
            +"id integer primary key autoincrement,"
            +"anthor text,"
            +"price real)";
    private Context mContext;
    public MyDataBaseHelper(Context context, String name, SQLiteDatabase.CursorFactory factory,int version) {
        super(context, name, factory, version);
        mContext = context;
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL(CREATE_BOOK);
        Toast.makeText(mContext,"create suceceed",Toast.LENGTH_LONG).show();
    }

    @Override
    public  void onUpgrade(SQLiteDatabase db,int oldVersion,int newVersion) {
    }
}

```

修改activity_main.xml中的代码，加入一个按钮用于创建数据库

```
<Button
        android:id="@+id/createDatabase"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Create Database"
        />

```

最后修改MainActivity中的代码，在onCreate()方法中构建了一个MyDatabaseHelper对象，在按钮的点击事件里调用了==getWritableDatabase()==方法

再次点击按钮时，会发现此时已经存在 BookStore.db数据库了，因此不会再创建一次

```
public class SQLiteActivity extends AppCompatActivity {

    private MyDataBaseHelper dbHelper;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sqlite);

        dbHelper = new MyDataBaseHelper(this,"BookStore.db",null,1);
        Button createdb = (Button) findViewById(R.id.createDatabase);
        createdb.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                dbHelper.getWritableDatabase();
            }
        });
    }
}

```

运行代码还需要借助一个叫作 Database Navigator的插件工具，File →Settings→Plugins→插件管理界面

![](https://img-blog.csdnimg.cn/img_convert/c37ee1c8f7fd174812ab13105edd4a6e.png)

然后进入/data/data/com.example.chapter6/databases/目录下，可以看到已经存在了一个 BookStore.db文件，BookStore.db文件右击→Save As，将它导出到你的计算机

![](https://img-blog.csdnimg.cn/img_convert/a11ef7c5a4aa758c64a5b394293856d7.png)

点开Android Studio的左侧边栏的DB Browser工具，点击这个工具左上角的加号按钮，并选择SQLite

![](https://img-blog.csdnimg.cn/img_convert/f63785d76a05f306a5bb629525d7616d.png)

后在弹出窗口的Database配置中选择我们刚才导出的BookStore.db文件

![](https://img-blog.csdnimg.cn/img_convert/82b0f8693a7bdfeecc73215a2ab43cef.png)

![](https://img-blog.csdnimg.cn/img_convert/0d70400063335068e838cc6e0f4787e2.png)

### 3.2 升级数据库

MyDatabaseHelper中的onUpgrade()方法是用于对数据库进行升级的

比如我们想在项目里再添加一张Category表用于记录分类，先在onCreate()方法里多加一条execSQL语句，然后在onUpgrade()方法中执行两条DROP语句，如果发现数据库中已经存在Book表或Category表，就将这两张表删除，然后调用onCreate()方法重新创建

修改自定义类MyDataBaseHelper，加入创建表的SQL语句，并且修改onCreate() 和 onUpgrade()

```
public static final String CREATE_CATEGORY = "create table Category ("
    +"id integer primary key autoincrement,"
    +"category_name text,"
    +"category_code integer)";

```

```
@Override
public void onCreate(SQLiteDatabase db) {
    db.execSQL(CREATE_BOOK);
    db.execSQL(CREATE_CATEGORY);
    Toast.makeText(mContext,"create suceceed",Toast.LENGTH_LONG).show();
}

@Override
public void onUpgrade(SQLiteDatabase db,int oldVersion,int newVersion) {
    db.execSQL("drop table if exists Book");
    db.execSQL("drop table if exists Category");
    onCreate(db);
}

```

修改MainActivity中的代码

SQLiteOpenHelper的构造方法里接收的第四个参数表示当前数据库的版本号，之前我们传入的是1，现在只要传入 一个比1大的数，就可以让onUpgrade()方法得到执行了

```
dbHelper = new MyDataBaseHelper(this,"BookStore.db",null,2);

```

现在重新运行程序，并点击“Create Database”按钮，这时就会再次弹出创建成功的提示