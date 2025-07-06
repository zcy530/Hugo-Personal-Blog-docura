---
title: React Native
slug: React-Native
lastmod: 2025-07-01T00:00:00+00:00
---

[https://www.reactnative.cn/docs](https://www.reactnative.cn/docs/textinput)

### 一、环境搭建

- React Native 简介
    
    **简介：**
    
    React native 是 react 的一个原声扩展，允许我们通过 react 的语法，来开发 ios 和 android 原生应用
    
    中文网：https://www.reactnative.cn/
    
    **React Native** **的优势：**
    
    1. 开发体验好：用统一的代码规范开发移动端程序，不用关注移动端的差异
    2. 开发成本低：开发一次，可以生成 Android 和 iOS 两个系统上的 App
    3. 学习成本低：只要掌握 JavaScript 和 react，就可以进行移动端开发了，否则，Android 这边我们还要学习 kotlin 和 java，ios 这边我们还要学习 swift 和 objective-C
    
    **React Native** **的不足：**
    
    1. 不成熟：项目版本和api更新频繁，学习成本高。有些问题较少解决方案，试错成本高
    2. 性能差：整体性能仍然不如原生
    3. 兼容性差：涉及底层的功能，需要针对 Android 和 iOS 双端单独开发
    
    **移动端 app 的开发模式：**
    
    ![Untitled](Untitled.png)
    
    ![Untitled](Untitled%201.png)
    
    **跨平台框架的比较：**
    
    ![Untitled](Untitled%202.png)
    
- 基础环境的搭建
    1. 安装 node.js，版本应该大于 12
        
        安装完之后可以配置国内的镜像，这样以后运行会快一些
        
        ```jsx
        npm config set registry https://registry.npm.taobao.org
        ```
        
    2. 安装 yarn
        
        ```jsx
        npm install -g yarn
        ```
        
    3. 安装 react native 脚手架
        
        ```jsx
        npm install -g react-native-cli
        ```
        
- 搭建 Android 环境
    
    首先了解安卓开发需要的工具
    
    ![](https://img-blog.csdnimg.cn/20200516095553968.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM3MTQ5MDYy,size_16,color_FFFFFF,t_70)
    
    ### 一、**安装 JDK**
    
    1. 搜索jdk，进入Oracle官网
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521121334351.png)
        
    2. 点击JDK download
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521121518531.png)
        
    3. 选择合适的版本和位数，此处以JDK11，win10，x64为例
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122000743.png)
        
    4. 下载完成后打开exe
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124037196.png)
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124157539.png)
        
    5. 打开cmd，输入java -version查看是否安装成功
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124326205.png)
        
    6. 这是安装好的场景，如果没有，可能需要配置环境变量
        
        此电脑–>属性->高级系统设置->环境变量->编辑
        
        添加好jdk的bin目录之后，一路点确认
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124637474.png)
        
    
    ### **二、安装 Android Studio**
    
    1. 进入Android官网[https://developer.android.google.cn/studio/](https://developer.android.google.cn/studio/)选择适合的版本进行download
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122142964.png)
        
    2. 双击下载的文件，进入安装界面，点击“next”进入下一步
        
        ![](https://pic1.zhimg.com/80/v2-0ae70036f6812b7bacc433e7efc0b59c_1440w.jpg)
        
    3. 一直点next直到安装成功，finish
        
        ![](https://pic4.zhimg.com/80/v2-881b97e059c9ae45f94926850b58d1b7_1440w.jpg)
        
    4. 在第一次运行时，若出现Unable to access Android SDK add-on list，表示Android Studio找不到Sdk，点击cancel 即可，没有什么大碍，等装好SDK后，自然就好了，下一步将会介绍如何安装SDK
        
        如果非常介意这个窗口，可以在 Android Studio 安装目录 bin/idea.properties 文件最后追加一句disable.android.first.run=true
        
    
    ### **三、安装 Android SDK**
    
    1. 在欢迎页点击 Configure -> SDK Manager
        
        或者在新建项目打开File -> Settings -> Appearance&Behavior -> System Settings -> Android SDK
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122913585.png)
        
    2. 点击SDK Update sites勾选Force https://..
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521123035164.png)
        
    3. 点击SDK Platforms，勾选Android10.0(Q)，和 Android sdk platform 29，点Apply，等待自动安装完成
        
        ![Untitled](Untitled%203.png)
        
    
    ### 四、配置环境变量
    
    1. Tools → SDK manager → 找到位置
        
        ![Untitled](Untitled%204.png)
        
    2. 配置环境变量
        
        ![Untitled](Untitled%205.png)
        
        ![Untitled](Untitled%206.png)
        
    3. 添加跟 ANDROID_HOME 相关的环境变量
        
        ![Untitled](Untitled%207.png)
        
    
    ### 五**、AVD配置（虚拟机）**
    
    1. 在欢迎页点击Configure -> AVD Manager，或者项目打开后点击 tools -> AVD Manager
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122913585.png)
        
    2. 选择普通电脑比较带的动的pixel2或者nexus S
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521125919662.png)
        
    3. 点击第一个download，等待安装
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521130007996.png)
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521130104241.png)
        
    4. 安装完成之后，点击上方的运行按钮，然后就可以运行你的第一个项目啦
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521130625812.png)
        
    
- 搭建 iOS 环境
- 初始化项目
    
    在命令行输入
    
    ```jsx
    react-native init myproject
    ```
    
    但是，在 init 中途出现了这样的错误，导致工程创建失败，里面仅有 node_modules，没有 Android、IOS 等文件
    
    ![Untitled](Untitled%208.png)
    
    产生这个问题的原因是：使用这种方式创建工程，在react-native 版本是0.69 版本上不适用。各位可以检查下自己安装的React-native的版本
    
    为了解决这个错误，我们要做的就是降级我们最新的 0.69 版本的 react native。要使用较旧的项目降级我们的项目，您必须执行以下命令
    
    可以将之前输入的命令改成：
    
    ```jsx
    npx react-native init chapter2 --version 0.68.2
    ```
    
    **创建成功！**
    
    ![Untitled](Untitled%209.png)
    
    **文件目录结构**
    
    ![Untitled](Untitled%2010.png)
    
    ![Untitled](Untitled%2011.png)
    
- 运行安卓模拟器
    
    ```jsx
    yarn android
    ```
    
    中间遇到的几个问题：
    
    1. ERROR: JAVA_HOME is set to an invalid directory: C:\Program Files\Java\jdk1.8.0_ 73\bin
    解决方法：修改 JAVA_HOME，把最后的 \bin 去掉
    [https://blog.csdn.net/u013933720/article/details/78363509](https://blog.csdn.net/u013933720/article/details/78363509)
    2. Android Gradle plugin requires Java 11 to run. You are currently using Java 1.8.
    解决方法：把 jdk 版本升级到 11
    [https://blog.csdn.net/technologyleader/article/details/127913029](https://blog.csdn.net/technologyleader/article/details/127913029)
    3. Failed to launch emulator. Reason: Emulator exited before boot en React Native when react-native run-android
    解决方法：现在 AVD manager 里面使用 cool boot
    [https://stackoverflow.com/questions/59495022/failed-to-launch-emulator-reason-emulator-exited-before-boot-en-react-native-w](https://stackoverflow.com/questions/59495022/failed-to-launch-emulator-reason-emulator-exited-before-boot-en-react-native-w)
    
    经过两天的折腾，终于成功了！
    
    ![Untitled](Untitled%2012.png)
    
- 下载便捷的 vscode 插件
    
    **ES7+ React/Redux/React-Native snippets**
    
    可以提供一些快速的代码编辑
    
    ![Untitled](Untitled%2013.png)
    
    rnc：react native clas
    
    ![Untitled](Untitled%2014.png)
    
    rnf：react native function
    
    ![Untitled](Untitled%2015.png)
    
- 调试工具
    1. 真机调试：打开 use 调试模式，通过 usb 线将电脑和手机连接起来
    2. 模拟器调试：安装在电脑上的虚拟的手机界面，一般跟随 Android studio 或者 xcode 一起安装，启动应用时模拟器会一起启动
        
        方法：键入 ctrl+m，选择 debug，自动跳转到浏览器
        
        ![Untitled](Untitled%2016.png)
        

### 二、基础知识

- 项目的基础文件
    1. index.js 入口文件
        
        ![Untitled](Untitled%2017.png)
        
        AppRegistry 是用来注册 app 的，有两个参数，第二个是回调函数
        
    2. App.js 里面是我们在模拟器上看到的页面
        
        ![Untitled](Untitled%2018.png)
        
        这些都是不用的，所以我们可以全部删掉，改成我们想要的页面，从 src 里面引入 Index 页面，然后 index 里面放置真正要写的页面样式，注意这个 Index 一定要大写，否则会报错！
        
        ![Untitled](Untitled%2019.png)
        
    3. package.json 配置文件
        
        ![Untitled](Untitled%2020.png)
        
    4. app.json 跟项目有关的信息
        
        ![Untitled](Untitled%2021.png)
        
    5. 创建的 src 文件夹，存放真正的页面样式的文件
        
        ![Untitled](Untitled%2022.png)
        
- 插值表达式
    
    
- 类组件与函数式组件
    
    **介绍：**
    
    你可以在 React 中使用函数式组件或 Class 组件。最开始只有 Class 组件能够使用 state ，但自从有了 React Hooks API, 就可以为函数组件添加 state 和很多其它的功能。Hooks API 是 React Native 0.59 提供的新特性, Hooks 是一种面向未来的编写 React 组件的方式，因此我们在本文档中优先使用函数组件，你也可以点击“Class 组件”切换到 Class 组件代码
    
    **类组件：**
    
    适合复杂的场景，有 state，有生命周期
    
    ```jsx
    import React, { Component } from 'react';
    import { Text, View } from 'react-native';
    
    class HelloWorldApp extends Component {
      render() {
        return (
          <View style={{
              flex: 1,
              justifyContent: "center",
              alignItems: "center"
            }}>
            <Text>Hello, world!</Text>
          </View>
        );
      }
    }
    
    export default HelloWorldApp;
    ```
    
    **函数式组件：**
    
    适合简单的场景，没有 state，没有生命周期(但是通过 hook 可以有)
    
    ```jsx
    import React from 'react';
    import { Text, View } from 'react-native';
    
    const HelloWorldApp = () => {
      let num = 100;
      return (
        <View style={{
            flex: 1,
            justifyContent: 'center',
            alignItems: 'center'
          }}>
          <Text>{num}</Text>
        </View>
      );
    }
    
    export default HelloWorldApp;
    ```
    
- 状态 state
- 属性 props
- 事件和 this 的指向
- 生命周期

### 三、组件和API

- StyleSheet
    
    stylesheet 是 RN 中声明样式的 API
    
    **与 css 一些不同：**
    
    1. 没有继承性，RN 当中的继承只发生在 text 组件上
    2. 样式名采用小驼峰命名 fontSize vs font-size
    3. 所有尺寸都是没有单位 width:100
    4. 有些特殊的样式名：marginHorizontal(水平外边距)，marginVertical(垂直外边距)
    
    **RN 样式的声明方式：**
    
    1. 通过 style 属性直接声明
        
        ```jsx
        <Text style={{fontSize: 30}}>content</Text>
        <Text style={[{fontSize: 30},{color: 'red'},{width: 100}]}>content</Text>
        ```
        
    2. 在 style 属性中调用 StyleSheet 声明的样式
        
        ```jsx
        引入： import {StyleSheet, View } from 'react-native'
        声明： const styles = StyleSheet.create({ 
                                redColor: {color: '#e33'}, 
                                fontLarge: {fontSize: 40} 
                        })
        使用： <View style={[styles.redColor, styles.fontLarge]}> content </view>
        ```
        
    
    **举例1**
    
    ![Untitled](Untitled%2023.png)
    
    **举例2**
    
    ![Untitled](Untitled%2024.png)
    
- StyleSheet 常用的样式属性
    
    **块级样式**
    
    paddingBottom
    
    paddingLeft
    
    paddingVertical
    
    marginBottom
    
    marginLeft
    
    marginTop
    
    borderRadius
    
    width
    
    height
    
    **布局相关：**
    
    alignItems
    
    justifyContent
    
    **字体相关：**
    
    fontSize
    
    fontWeight
    
    color
    
- Flexbox 弹性布局
    
    **Flexbox 的术语了解：**
    
    1. container：采用 flex 布局的元素，成为 flex container
    2. item：容器 container 中的所有子元素，成为 flex item
    3. main axis：主轴
    4. cross axis：交叉轴
    
    **弹性布局的模型**
    
    web 开发当中的 flexbox
    
    ![Untitled](Untitled%2025.png)
    
    RN 开发当中的 flexbox，轴的方向发生了变化
    
    ![Untitled](Untitled%2026.png)
    
- Flexbox 的五种属性
    
    **Flexbox 的属性：**
    
    - flexDirection：声明主轴方向，row 是 web 默认，column 是 RN 默认
    - justifyContent：声明 item 在主轴上的对齐方式
    - alignItems：声明 item 在交叉轴上的对齐方式
    - flex：声明 item 在主轴上的尺寸比例
    - flexWrap：是否自动换行，wrap | noWrap | wrap-reverse
    
    **flexDirection：主轴方向**
    
    可选项有 column(默认) | column-reverse | row | row-reverse
    
    ![Untitled](Untitled%2027.png)
    
    ![Untitled](Untitled%2028.png)
    
    ![Untitled](Untitled%2029.png)
    
    ![Untitled](Untitled%2030.png)
    
    **justifyContent：主轴对齐方式**
    
    可选项：flex-start(默认) | center | flex-end | space-around 空格环绕 | space-evenly 空格平均分布 | space-between 两端对齐
    
    ![Untitled](Untitled%2031.png)
    
    ![Untitled](Untitled%2032.png)
    
    **alignItems：交叉轴对齐方式**
    
    可选项：flex-start(默认) | center | flex-end |stretch | baseline 机械对齐
    
    ![Untitled](Untitled%2033.png)
    
    ![Untitled](Untitled%2034.png)
    
    **flex：尺寸比例**
    
    ![Untitled](Untitled%2035.png)
    
- 响应式布局 flexbox + Dimensions
    
    因为现在的手机尺寸五花八门，我们没有必要根据每一种尺寸做定制化的开发，所以响应式布局非常有必要。响应式布局要用到的：flexbox，Dimensions
    
    flexbox 的主要作用是弹性布局
    
    Dimensions 的主要作用是获取屏幕的尺寸，就是高度和宽度
    
    **Dimensions 的使用**
    
    引入模块
    
    ```jsx
    import { Dimensions } from 'react-native'
    ```
    
    获取屏幕尺寸
    
    ```jsx
    const windowWidth = Dimensions.get('window').width;
    const windowHeight = Dimensions.get('window').height;
    ```
    
    **实践演示：**
    
    引入 Dimensions
    
    ![Untitled](Untitled%2036.png)
    
    最重要的是这里的除以三，想要几列就除以几就行
    
    ![Untitled](Untitled%2037.png)
    
- 组件和 API 简介
    
    **核心组件简介**
    
    RN 中的核心组件，是对原生组件的封装
    
    原生组件：Android 或者 iOS 内的组件
    
    核心组件：RN 中最常用的，相当于 html 的标签，来自 react-native 的组件。有很多类型划分，比如基础组件、交互组件、列表视图、iOS 独有组件、Android 独有组件、其他
    
    ![Untitled](Untitled%2038.png)
    
    ![Untitled](Untitled%2039.png)
    
    ![Untitled](Untitled%2040.png)
    
    **核心组件**
    
    | View | 视图组件 |
    | --- | --- |
    | Text | 文本组件 |
    | Alert | 警告框组件 |
    | Button | 按钮组件 |
    | Switch | checkbox组件 |
    | StatusBar | 状态栏组件 |
    | ActivityIndicator | 加载提示器组件 |
    | Image | 图片组件 |
    | TextInput | 输入框组件 |
    | Touchable | 触碰组件 |
    | ScrollView | 滚动视图组件 |
    | SectionList | 分组列表组件 |
    | FlatList | 高性能组件 |
    | Animated | 动画组件 |
    
- Button 和 Alert
    
    **Button 属性的值**
    
    | 属性 | 含义 | 内容 |
    | --- | --- | --- |
    | title | 按钮上面的文字 | 字符串 |
    | onPress | 单击事件 | 回调函数 |
    | color | 按钮的颜色 | {‘red’} |
    
    **Button 使用的示例** 
    
    ```jsx
    export default class index extends Component {
      createTwoButtonAlert = () => {
        Alert.alert(
          "My Title",
          "My Content",
          [
            {
              text: "Cancel!",
              onPress: () => console.log('cancel'),
              style: 'cancel'
            },
            {
              text: "Yes!",
              onPress: () => console.log('OK'),
              style: 'default'
            }
          ]
        )
      }
    
      createThreeButtonAlert = () => {
        Alert.alert(
          "更新提示",
          "发现新版本，是否现在更新",
          [
            {
              text: "稍后再试",
              onPress: () => console.log('later'),
              style: 'default'
            },
            {
              text: "取消",
              onPress: () => console.log('cancel'),
              style: 'cancel'
            },
            {
              text: "确认",
              onPress: () => console.log('OK'),
              style: 'default'
            }
          ]
        )
      }
      render() {
        return (
          <View style={[styles.container]}>
    
            <Button 
              title="alert1"
              onPress={()=>{
                alert('直接调用alert函数')
              }}
            />
            <Button 
              title="alert2"
              onPress={()=>{
                Alert.alert('调用Alert组件')
              }}
              color={'red'}
            />
            <Button 
              title="两个button"
              onPress={this.createTwoButtonAlert}
              color={'green'}
            />
            <Button 
              title="三个button"
              onPress={this.createThreeButtonAlert}
              color={'green'}
            />
          </View>
        )
      }
    }
    ```
    
    ![Untitled](Untitled%2041.png)
    
- Modal
    
    **作用：**原生有 Dialog，Toast 之类的弹窗控件，React-Native 虽然也有 Dialog，但是并不好用，所幸有 Modal 这个组件，使用起来简单，而且还比较好用
    
    **常用属性：**
    
    | animationType
     | 设置Modal的出现方式，有3个参数 | slide ：从底部弹出、fade ： 淡入视野、none： 出现没有动画 |
    | --- | --- | --- |
    | onRequestClose | Modal关闭时调用此方法 | onRequestClose={() => console.log('onRequestClose...')} |
    | onShow | 当modal显示时，可以传递一个函数用来调用 |  |
    | transparent | 使Modal的背景色透明 |  |
    | visible | 用来控制Modal是否可见 ture / false |  |
    
- StatuBar
    
    **StatuBar 对应的组件**
    
    是手机最顶部的状态栏，显示时间、消息、网络情况等
    
    ![Untitled](Untitled%2042.png)
    
    **StatuBar 的属性**
    
    | 属性 | 含义 | 值 |
    | --- | --- | --- |
    | hidden | 是否隐藏 | ={false} ={true} |
    | backgroundColor | 背景颜色 | =”red” |
    | barStyle | 样式 | ={’dark-content’} |
- Switch
    
    **Switch 对应的组件**
    
    这种小型的开关，相当于 checkbox
    
    ![Untitled](Untitled%2043.png)
    
    **Switch 的属性**
    
    | 属性 | 含义 | 值 |
    | --- | --- | --- |
    | trackColor | 背景的颜色 | ={{false:’red,true:’green’}} |
    | thumbColor | 按钮的颜色 | ={’blue’} |
    | value | 控制的值 | ={this.state.name} |
    | onValueChange | 控制值的变化函数 | ={this.toggleStatusBar} |
    
    **举例：**
    
    通过 switch 按钮来操作 statusBar 的显示/隐藏
    
    ![Untitled](Untitled%2044.png)
    
    ![Untitled](Untitled%2045.png)
    
- ActivityIndicator
    
    **ActivityIndicator 的作用：**
    
    展示等待的状态，在安卓和ios上的显示是不一样的
    
    ![Untitled](Untitled%2046.png)
    
    **ActivityIndicator 的使用**：
    
    引入
    
    ```jsx
    import { ActivityIndicator ****} from 'react-native'
    ```
    
    使用
    
    ```jsx
    <ActivityIndicator color="blue" size={'large'} />
    <ActivityIndicator color="green" size={'small'} />
    // 数字指定大小，旨在 android 应用下有效
    <ActivityIndicator color="#00d0ff" size={70} />
    <ActivityIndicator color="red" size={100} />
    ```
    
    常用属性
    
    | color | 颜色 | =“blue” |
    | --- | --- | --- |
    | size | 大小 | ={’large’} ={70} |
- Platform
    
    作用：Platform 可以判断当前用户使用的手机的系统
    
    引入：
    
    ```jsx
    import { Platform } from 'react-native'
    ```
    
    使用：
    
    ```jsx
    **Platform.OS**
    
    if(Platform.OS === 'android'){
        alert('android')
    } else if(Platform.OS === 'ios'){
        alert('iosw')
    }
    ```
    
- Image
    
    **作用**：加载图片
    
    **加载方式**：本地路径、图片的 URI 地址、图片的 Base64 字符串
    
    **常用属性**:
    
    | style | 样式 | ={[styles.ItemImage]} |
    | --- | --- | --- |
    | source | 图片的路径 | ={require(’/images/01.png’)} |
    
    **使用举例：**
    
    ```jsx
    <Image
      source={{uri: 'https://reactnative.dev/docs/assets/p_cat2.png'}}
      style={{ width: 200, height: 200 }}
    />
    <Image
      source={require(’/images/01.png’)}
      style={[styles.itemImage]}
    />
    ```
    
    ![Untitled](Untitled%2047.png)
    
- TextInput
    
    **作用：**
    
    TextInput 是一个允许用户在应用中通过键盘输入文本的基本组件。本组件的属性提供了多种特性的配置，譬如自动完成、自动大小写、占位文字，以及多种不同的键盘类型（如纯数字键盘）等等
    
    **使用方法：**
    
    最简单的用法就是丢一个 TextInput 到应用里，然后订阅它的 onChangeText事件来读取用户的输入。注意，从 TextInput 里取值这就是目前唯一的做法！也就是使用在 onChangeText 中用 setState 用户的输入写入到 state 中，然后在需要取值的地方从 this.state 中取出值。它还有一些其它的事件，譬如 onSubmitEditing 和 onFocus
    
    **组件的属性：**
    
    | style | 样式 | ={[styles.input]} |
    | --- | --- | --- |
    | placeholder | 默认的值 | =“please input” |
    | placeholderTextColor | 默认字体颜色 | ="rgba(173, 186, 204, 1)” |
    | defaultValue | 默认的值 | ="You can type in me” |
    | style | 样式文件 | ={styles.habitInput} |
    | onChangeText | 当文本框内容变化时调用此回调函数 | ={(val)⇒{
     this.setState({
       username:val
     })
    }} |
    | secureTextEntry | 是否为密码框 | ={true} |
    | keyboardType | 键盘类型 | =”number-pad” |
    | inlineImageLeft | 指定一个图片放置在左侧 |  |
    | autoFocus | 自动对焦 | ={true} |
    
    **使用示例：**
    
    ![Untitled](Untitled%2048.png)
    
- Touchable
    
    **Touchable 的作用**：封装视图，使其可以正确响应触摸操作。
    
    **TouchableHighlight**：触碰后，高亮显示
    
    ![Untitled](Untitled%2049.png)
    
    **TouchableOpacity**：触碰后，透明度降低(模糊显示)
    
    ![Untitled](Untitled%2050.png)
    
    **TouchableWithoutFeedback**：触碰后，没有任何相应
    
    ![Untitled](Untitled%2051.png)
    
- ScrollView
    
    **作用：**滚动视图，显示超出可视区域的内容
    
    **属性：**
    
    | contentContainerStyle | 样式会应用到内容容器 | ={styles.contentContainer} |
    | --- | --- | --- |
    | showsVerticalScrollIndicator | 是否显示垂直方向的滚动条 | ={true} |
    | showsHorizontalScrollIndicator | 是否显示水平方向的滚动条 | ={true} |
    | horizontal | 所有的子视图会在水平方向上排成一行 | 默认 ={false} |
    
    **使用的示例：**
    
    ![Untitled](Untitled%2052.png)
    
    ![Untitled](Untitled%2053.png)
    
    **一个 ScrollView 的 bug 解决方案：**
    
    如何解决 Android 开发时 ScrollView 滚动不到底的问题
    
    ```jsx
    <ScrollView>
      <View> style={{height: Platform.OS === 'ios' ? 0 : 100}}</View>
    </ScrollView>
    ```
    
- SafeAreaView
    
    作用：自动避开刘海屏，所以以后开发建议使用 SafeAreaView
    
    ![Untitled](Untitled%2054.png)
    
- SectionList
    
    作用：高性能的分组列表组件，支持单独的头部组件，支持单独的尾部组件，支持分组的头部组件，支持分组的分隔线，支持自定义行间分隔线，支持下拉刷新，支持上拉加载
    
- FlatLit
    
    作用：也是用来展示一个列表，跟 SectionList 不同，它不能进行分组
    
- Animated
    
    **定义：**
    
    动画组件，RN 中可以直接使用的动画组件
    
    - Animated.View
    - Animated.Text
    - Animated.ScrollView
    - Animated.Image
    
    **如何创建动画：**
    
    1. 创建初始值
        
        ```jsx
        Animated.Value() 单个值
        Animated.ValueXY() 向量值
        ```
        
    2. 将初始值绑定在动画组件上，一般将其绑定到某个样式属性上，例如：opacity，translate
    3. 通过动画类型 api，一帧一帧的更改初始值
        
        ```jsx
        Animated.decay() 加速效果
        Animated.spring() 弹跳效果
        Animated.timing() 时间渐变效果
        ```
        
    
    **例子：**
    
    用5秒的时间，把一个图像的透明度从0变成1
    
    ```jsx
    import React, { useRef } from "react";
    import { Animated, Text, View, StyleSheet, Button } from "react-native";
    
    const App = () => {
      // 设置初始值为0
      const fadeAnim = useRef(new Animated.Value(0)).current;
    
      const fadeIn = () => {
        // Will change fadeAnim value to 1 in 5 seconds
        Animated.timing(fadeAnim, {
          toValue: 1, // 目标值
          duration: 5000,  // 动画执行时间
                 useNativeDriver: true // 启用原生方式渲染动画
        }).start();
      };
    
      const fadeOut = () => {
        // Will change fadeAnim value to 0 in 5 seconds
        Animated.timing(fadeAnim, {
          toValue: 0,
          duration: 5000,
               useNativeDriver: true // 启用原生方式渲染动画
        }).start(() => {
                        alert("done") // 动画执行结束之后的回调函数
             });
      };
    
      return (
        <View style={styles.container}>
    
          <Animated.View
            style={[
              styles.fadingContainer,
              {
                opacity: fadeAnim // Bind opacity to animated value
              }
            ]}
          >
            <Text style={styles.fadingText}>Fading View!</Text>
          </Animated.View>
    
          <View style={styles.buttonRow}>
            <Button title="Fade In" onPress={fadeIn} />
            <Button title="Fade Out" onPress={fadeOut} />
          </View>
        </View>
      );
    }
    
    const styles = StyleSheet.create({
      container: {
        flex: 1,
        alignItems: "center",
        justifyContent: "center"
      },
      fadingContainer: {
        paddingVertical: 8,
        paddingHorizontal: 16,
        backgroundColor: "powderblue"
      },
      fadingText: {
        fontSize: 28,
        textAlign: "center",
        margin: 10
      },
      buttonRow: {
        flexDirection: "row",
        marginVertical: 16
      }
    });
    
    export default App;
    ```
    
- NativeModules
    
    作用：在用 React Native 开发 App 时会用到一些原生模块，比如：在做社会化分享、第三方登录、扫描、通信录，日历等等，关于在React Native中使用原生模块，在这里引用React Native官方文档的一段话：
    
    > 有时候App需要访问平台API，但在React Native可能还没有相应的模块。或者你需要复用一些Java代码，而不想用JavaScript再重新实现一遍；又或者你需要实现某些高性能的、多线程的代码，譬如图片处理、数据库、或者一些高级扩展等等。
    > 
    > 
    > 我们把React Native设计为可以在其基础上编写真正的原生代码，并且可以访问平台所有的能力。这是一个相对高级的特性，我们并不期望它应当在日常开发的过程中经常出现，但它确实必不可少，而且是存在的。如果React Native还不支持某个你需要的原生特性，你应当可以自己实现对该特性的封装。
    > 
    
    访问状态栏的属性：
    
    ```jsx
    const {StatusBarManager} = NativeModules;
    
    StatusBarManager.HEIGHT
    ```
    

### 四、外部组件库

- LinearGradient
    
    **作用：**渐变组件
    
    **引入：**
    
    ```jsx
    npm i react-native-linear-gradient
    ```
    
    **从上到下的渐变：**默认的，属性是 color
    
    ```jsx
    <LinearGradient 
        colors={['#63B8FF', '#1C86EE', '#0000EE',]} 
        style={{height: 150}}/>
    ```
    
    **从左到右的渐变**：start/end
    
    ```jsx
    start:{ x: number, y: number } start 就是渐变开始的位置，x、y 范围是 0 ~ 1 
    end:{ x: number, y: number } end 同上，就是渐变结束的位置
    ```
    
    **设定颜色的比例：**location
    
    如果想指定每种渐变颜色的范围，比如红色占20%， 绿色占70%，黑色占10%，也是可以设置的，就用到了另外一个属性：locations。locations 对应的是 colors
    
    ```jsx
    locations={[0.2,0.7,1.0]}
    colors={['red', 'green', 'black']}
    
    以上代码的含义如下：
    red 范围就是 0.0 - 0.2；
    green 范围就是 0.2 - 0.7；
    black 范围就是 0.7 - 1.0；
    ```
    
    **示例：**斜角渐变
    
    start: { x: 0.25, y: 0.4 } 渐变是从左侧25%，上部40%开始
    
    end: { x: 0.7, y: 0.8 } 渐变是从左侧70%，上部80%结束
    
    ```jsx
    <LinearGradient
        start={{x: 0.25, y: 0.25}}
        end={{x: 0.75, y: 0.75}}
        colors={['red', 'green', 'black']}
        style={{height: 150, flex: 1}}/>
    ```
    
    **示例：**从左到右渐变
    
    ```jsx
    <LinearGradient
        start={{x: 0, y: 0}} 
        end={{x: 1, y: 0}}
        colors={['red', 'green', 'black']}
        style={{height: 150, flex: 1}}/>
    ```
    
- ScaledSheet, verticalScale
    
    **react-native-size-matters:** 一个轻量级的、零依赖性的React-Native实用工具带，用于在不同大小的设备上扩展应用程序 UI 的大小。当使用 react-native 开发时，你需要手动调整你的应用程序，使其在各种不同的屏幕尺寸上看起来都很棒。那是一份乏味的工作。react-native-size-matters 提供了一些简单的工具，使您的扩展更加容易。其想法是在标准的 5 英寸屏幕移动设备上开发一次，然后简单地应用提供的 util
    
    **安装：**
    
    ```jsx
    npm install --save react-native-size-matters
    ```
    
    **使用方法：**
    
    - scale(size: number)将根据设备的屏幕宽度返回所提供大小的线性缩放结果
    - verticalScale(size: number)将根据设备的屏幕高度返回所提供大小的线性缩放结果
    - moderateScale(size: number, factor?: number)有时候你不想以线性的方式来扩展每件事，这就是适度比例的由来。很酷的一点是，您可以控制调整大小因子（默认值为0.5）。如果“正常比例”将使您的大小增加2倍，则“中等比例”仅将其增加2倍，例如：比例（10）=20，中等比例（10）=15，中等比例（10，0.1）=11
    - moderateVerticalScale(size: number, factor?: number)与中等比例相同，但使用垂直比例而不是比例。
    
    ```jsx
    import { 
    scale, 
    verticalScale, 
    moderateScale, 
    moderateVerticalScale 
    } from 'react-native-size-matters';
    或者 import { s, vs, ms, mvs } from 'react-native-size-matters'; （速记的方法）
    
    const Component = props =>
        <View style={{
            width: scale(30),
            height: verticalScale(50),
            padding: moderateScale(5)
        }}/>;
    
    ```
    
    **ScaledSheet**
    ScaledSheet将采用与常规样式表相同的样式对象，外加一个特殊（可选）注释，该注释将自动为您应用缩放函数
    
    - @s将scale函数应用于size。
    - @vs将verticalScale函数应用于size。
    - @ms将在size上应用大小因子为0.5的moderateScale函数。
    - @mvs将在size上应用大小因子为0.5的moderateVerticalScale函数。
    - @ms<factor>将应用moderateScale函数，其大小调整因子为factor。
    - @mvs<factor>将应用moderateVerticalScale函数，其大小调整因子为factor。
    
    ```jsx
    import { ScaledSheet } from 'react-native-size-matters';
    
    const styles = ScaledSheet.create({
        container: {
            width: '100@s', // = scale(100)
            height: '200@vs', // = verticalScale(200)
            padding: '2@msr', // = Math.round(moderateScale(2))
            margin: 5
        },
        row: {
            padding: '10@ms0.3', // = moderateScale(10, 0.3)
            width: '50@ms', // = moderateScale(50)
            height: '30@mvs0.3' // = moderateVerticalScale(30, 0.3)
        }
    });
    ```
    
- DateTimePicker
    
    虽然之前的 react-native-datepicker 很好用，但是我们如果现在使用话，会给出警告信息，告诉我们现在推出了新版本的，集成了 IOS 和 Android 的新插件，datepicker 未来将会不可用。所以要及时了解其替代品 @react-native-community/datetimepicker
    
    ```jsx
    npm install @react-native-community/datetimepicker --save
    yarn add @react-native-community/datetimepicker
    ```
    
    使用：
    
    ```jsx
    import DateTimePicker from "@react-native-community/datetimepicker"
    
    <DateTimePicker
      value={date}
      mode="date"
      minimumDate={new Date(1950, 0, 1)}
      maximumDate={new Date()}
        is24Hour={true}
      display="spinner"
      onChange={onChangeTime}
      />
    ```
    
    常用的属性：
    
    | value | value 值必填，且必须是 Date 日期对象类型 |
    | --- | --- |
    | mode | “date" 默认、“time”、“datetime” (iOS only)、“countdown” (iOS only) |
    | is24Hour | ={true} |
    | display | 是显示的样式，有四种
    “default”、“spinner”、“calendar” (only for date mode)、“clock” (only for time mode) |
    | minimumDate、maximumDate | 分别是可选择的最大日期和最小日期，注意也是Date类型的 |
- DragSortableView
    
    安装
    
    ```jsx
    npm install react-native-drag-sort
    ```
    
    导入
    
    ```jsx
    import { DragSortableView } from 'react-native-drag-sort';
    ```
    
    使用
    
    ```jsx
    {/* 拖拽组件 */}
    <DragSortableView
        dataSource={myCategorys}//数据源
        fixedItems={[0, 1]}//指定下标不可拖拽
        renderItem={(item, index) => {//item样式
            return (
                //注意：item不能再次包裹触摸事件，他已经包裹了
                // <Touchable key={item.id} onPress={() => this.onItemClick(item, index, true)}>
                <ItemView
                    isEdit={isEdit}
                    selected={true}
                    disabled={index < 2}
                    data={item} />
                // </Touchable>
            )
        }}
        sortable={isEdit}//什么时候可以拖拽
        keyExtractor={item => item.id}
        onDataChange={this.onDataChange}//拖拽排序
        parentWidth={parentWidth}//拖拽区域的宽度
        childrenWidth={itemWidth}//item的宽度
        childrenHeight={itemHeight}//item的高度
        marginChildrenTop={marginTop}//item的上边距
        onClickItem={(data: CategoryType[], item: CategoryType) => {
            //item的点击事件
            this.onItemClick(item, data.indexOf(item), true)
        }}
    />
    
    //拖拽排序
    onDataChange = (data: CategoryType[]) => {
        this.setState({
            myCategorys: [...data]
        })
    }
    ```
    
- Icon
    
    **定义：**react-native-vector-icons 是 rn 项目采用 iconfont 的工具库。那么问题来了，iconfont 是什么？简单说，就是我们平时用的字体，不再是我们传统认知上的“文字”，而是一个个的图标。关于 rn 项目如何添加 react-native-vector-icons，不进行说明，请参照 [react-native-vector-icons](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Foblador%2Freact-native-vector-icons)
    
    **意义：**不知道什么时候开始， iconfont 成为了 App 开发的利器，不仅因为它是矢量图标，可以轻松解决图标适配和颜色问题，而且它是以字体文件的形式存在项目中，比起常规图片更能节省 App 的体积，而 react-native-vector-icons 是在 GitHub 上最火的 React Native 的 iconfont 图标库，也是这博客的主角。
    
    **引入：**
    
    ```jsx
    npm install --save react-native-vector-icons
    
    // 或者
    npm install -g yarn
    yarn add react-native-vector-icons
    ```
    
    **Android 平台上的配置**
    
    ```jsx
    // 自动配置
     react-native link react-native-vector-icons
    
     // 或者
     npm install -g rnpm
     rnpm link react-native-vector-icons
    ```
    
    这个脚本命令可以帮你自动配置好，如果是运行成功的情况下，可惜往往都是失败的。如果这步成功了，而且能够正常运行，下面这些就可以忽略了
    
    **使用方法：**
    
    ```jsx
    import Icon from 'react-native-vector-icons/FontAwesome';
    import Ionicons from 'react-native-vector-icons/Ionicons';
    import AntDesign from 'react-native-vector-icons/AntDesign';
    import MaterialCommunityIcons from 'react-native-vector-icons/MaterialCommunityIcons';
    import Octicons from 'react-native-vector-icons/Octicons';
    ```
    
    ```jsx
    <Icon 
      name="rocket" 
      size={30} 
      color="#900" 
    />
    <Ionicons
      name="close"
      size={16}
      color="rgba(173, 186, 204, 1)"
    />
    <Ionicons
        name="caret-down-circle"
        size={18}
        color="rgba(173, 186, 204, 1)"
    />
    
    <AntDesign
      name="clockcircle"
      size={16}
      color="rgba(19, 57, 102, 1)"
    />
    <AntDesign
      name="pausecircleo"
      size={22}
      color="red"
    />
    
    <MaterialCommunityIcons
      name="drag"
      size={32}
      color="rgba(196, 196, 196, 1)"
    />
    
    <MaterialCommunityIcons
      name="drag"
      size={32}
      color="rgba(196, 196, 196, 1)"
    />
    
    <Octicons
      name="arrow-switch"
      size={15}
      color="rgba(173, 186, 204, 1)"
      style={styles.switchIcon}
    />
    <Octicons
      name="arrow-switch"
      size={15}
      color="rgba(173, 186, 204, 1)"
      style={styles.switchIcon}
    />
    ```
    
- Video

### 五、路由与导航 React-Navigation

- 安装下载
    
    安装包
    
    ```jsx
    yarn add @react-navigation/native
    ```
    
    安装必要的依赖
    
    ```jsx
    yarn add react-native-renimated (动画增强)
    yarn add react-native-gesture-handler
    yarn add react-native-screens (屏幕处理)
    yarn add react-native-safe-area-context (处理安全区域)
    yarn add @react-native-community/masked-view
    ```
    
    链接：RN 0.6 之后安卓环境自动链接路由，Android 无需任何操作，iOS 下需要手动链接路由
    
- NavigationContainer
    
    添加头部组件，放到应用的头部(index.js/App.js)
    
    ```jsx
    import 'react-native-gesture-handler'
    ```
    
    添加导航容器，我们需要在入口文件中，把整个应用包裹在导航容器NavigationContainer 中 
    
    ```jsx
    import 'react-native-gesture-handler'
    import * as React from 'react'
    import { NavigationContainer } from '@react-navigation/native'
    
    export default function App() {
     return (
            <NavigationContainer>
                {/* 具体应用的代码 */}
            </NavigationContainer>
     )
    }
    ```
    
- StackNavigation
    
    **简介**
    
    RN 中默认没有类似浏览器 history 对象，在 RN 中跳转之前，要先将路由声明在 Stack 中，才能实现跳转
    
    **安装**
    
    ```jsx
    yarn add @react-navigation/stack
    ```
    
    使用
    
    ```jsx
    import { createStackNavigator } from '@react-navigation/stack'
    
    const Stack = createStackNavigator();
    ```
    
    | Stack.Navigation | 作用于整个导航，包含多个屏幕 |
    | --- | --- |
    | initialRouteName | 初始化路由，默认加载的路由 |
    | headerMode | 声明头部显示的信息 |
    | screenOptions | 也可以声明一些属性 |
    | Stack.Screen | 仅仅作用于当前屏幕 |
    | name | 路由的名称 |
    | component | 路由对应的组件的内容 |
    | title | 标题 |
    | headerTitleStyle | 头部的风格 |
    | headerLeft | 头部左边 |
    | headerRight | 头部右边 |
    
    ```jsx
    import * as React from 'react';
    import { NavigationContainer } from '@react-navigation/native';
    import { createStackNavigator } from '@react-navigation/native-stack';
    
    function HomeScreen({ prop }) {
        return (<Button onPress={() => prop.navigation.navigate('details')} />)
    }
    function DetailsScreen({ prop }) {
        return (<Button onPress={() => prop.navigation.navigate('home')} />)
    }
    
    const Stack = createStackNavigator();
    
    function App() {
      return (
          <NavigationContainer>
            <Stack.Navigator
              initialRouteName='home'
              screenOptions={{
                headerShown: false,
                navigationBarHidden: true, 
                navigationBarColor: 'rgba(0,0,0,0)',
              }}
               >
              <Stack.Screen name="home" component={HomeScreen} />
              <Stack.Screen name="details" component={DetailsScreen} />
    
            </Stack.Navigator>
          </NavigationContainer>
      );
    }
    
    export default App;
    ```
    
- BottomTabNavigation
    
    简介：底部选项卡的导航效果
    
    安装
    
    ```jsx
    yarn add @react-navigation/bottom-tabs
    ```
    
    使用
    
    ```jsx
    import { createBottomTabNavigator } from '@react-navigation/bottom-tabs'
     
    const Tab = createBottomTabNavigator();
    
    export default function App() {
        return(
            <NavigationContainer>
                <Tab.Navigator>
                  <Tab.Screen name="Home" component={HomeScreen} />
                    <Tab.Screen name="Settings" component={SettingsScreen} />
                </Tab.Navigator>
            </NavigationContainer>
        )
    }
    ```
    
    具体
    
    ```jsx
    import { ParamListBase, RouteProp } from '@react-navigation/native';
    import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
    import { Text, TouchableWithoutFeedback, View, Image } from 'react-native';
    
    const HomeNavigationTab = createBottomTabNavigator();
    
    {/* 以下是定义每一页的内容 */}
    function HomeScreen() {
        return (
            <View style={{ flex: 1 }}>
               <Home />
            </View>
        );
    }
    
    function EaseScreen() {
        return (
            <View style={{ flex: 1 }}>
                <HabitTemplatePage />
            </View>
        );
    }
    
    function ExploreScreen() {
        return (
            <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
                <Text style={{ fontSize: 28 }}>Explore Page</Text>
            </View>
        );
    }
    
    function MeScreen() {
        return (
            <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
                <Text style={{ fontSize: 28 }}>Me Page</Text>
            </View>
        );
    }
    
    {/* 以下是定义导航栏的路由 */}
    const HomeIndex = () => {
        return (
            <HomeNavigationTab.Navigator
                screenOptions={({ route }) => ({
                    tabBarActiveTintColor: 'rgba(61, 148, 255, 1)',
                    tabBarInactiveTintColor: 'gray',
                    headerShown: false,
                    tabBarStyle: {
                        height: rpx(100),
                        borderTopWidth: 0,
                    }
                })}>
                <HomeNavigationTab.Screen
                    name="day"
                    component={HomeScreen}
                    options={(navigation) => ({
                        tabBarLabel: '今日',
                        tabBarIcon: ({ focused, size }) => (
                            <HomeNavigationTabItem
                                navigation={navigation.navigation}
                                route={navigation.route}
                                foucs={focused} />
                        ),
                    })} />
                <HomeNavigationTab.Screen
                    name="ease"
                    component={EaseScreen}
                    options={(navigation) => ({
                        tabBarLabel: '平和',
                        tabBarIcon: ({ focused, size }) => (
                            <HomeNavigationTabItem
                                navigation={navigation.navigation}
                                route={navigation.route}
                                foucs={focused} />
                        ),
                    })} />
                <HomeNavigationTab.Screen
                    name="explore"
                    component={ExploreScreen}
                    options={(navigation) => ({
                        tabBarLabel: '探索',
                        tabBarIcon: ({ focused, size }) => (
                            <HomeNavigationTabItem
                                navigation={navigation.navigation}
                                route={navigation.route}
                                foucs={focused} />
                        ),
                    })} />
                <HomeNavigationTab.Screen
                    name="me"
                    component={MeScreen}
                    options={(navigation) => ({
                        tabBarLabel: '我的',
                        tabBarIcon: ({ focused, size }) => (
                            <HomeNavigationTabItem
                                navigation={navigation.navigation}
                                route={navigation.route}
                                foucs={focused} />
                        ),
                    })} />
            </HomeNavigationTab.Navigator>
        );
    };
    
    {/* 以下是定义底部导航栏的按钮和图标样式 */}
    const HomeNavigationTabItem = (props: {
        route: RouteProp<ParamListBase, string>;
        navigation: any;
        foucs: boolean;
    }) => {
    
        switch (props.route.name) {
            case 'day':
                return (
                    <TouchableWithoutFeedback onPress={() => { props.navigation.navigate('day') }}>
                        <View style={{ flexDirection: "column", paddingTop: rpx(16), paddingBottom: rpx(8) }}>
                            <Image source={Theme.getValue('$iconDaySun')} style={{ width: rpx(42), height: rpx(42) }}></Image>
                        </View>
                    </TouchableWithoutFeedback>
                )
            case 'ease':
                return (
                    <TouchableWithoutFeedback onPress={() => { props.navigation.navigate('ease') }}>
                        <View style={{ flexDirection: "column", paddingTop: rpx(16), paddingBottom: rpx(8) }}>
                            <Image source={Theme.getValue('$iconEaseHeart')} style={{ width: rpx(42), height: rpx(42) }}></Image>
                        </View>
                    </TouchableWithoutFeedback>
                )
            case 'explore':
                return (
                    <TouchableWithoutFeedback onPress={() => { props.navigation.navigate('explore') }}>
                        <View style={{ flexDirection: "column", paddingTop: rpx(16), paddingBottom: rpx(8) }}>
                            <Image source={Theme.getValue('$iconExploreSafari')} style={{ width: rpx(42), height: rpx(42) }}></Image>
                        </View>
                    </TouchableWithoutFeedback>
                )
            case 'me':
                return (
                    <TouchableWithoutFeedback onPress={() => { props.navigation.navigate('me') }}>
                        <View style={{ flexDirection: "column", paddingTop: rpx(16), paddingBottom: rpx(8) }}>
                            <Image source={Theme.getValue('$iconMeHuman')} style={{ width: rpx(42), height: rpx(42) }}></Image>
                        </View>
                    </TouchableWithoutFeedback>
                )
            default:
                return (<View></View>)
        }
    }
    
    export default HomeIndex;
    ```
    
- 路由嵌套
    
    简介：在一个导航的内部，可以渲染另一个导航
    
    ![Untitled](Untitled%2055.png)
    
- 路由传参
    
    **传递参数**
    
    ```jsx
    navigation.navigate('name',{key:123})
    ```
    
    **接收参数**
    
    ```jsx
    类组件
    this.props.route.params.KEY 
    
    函数式组件
    route.params.KEY
    ```
    

### 六、状态管理 mobx

- mobx 简介
    
    mobx 是 react 中的全局数据管理库，可以简单的实现数据的跨组件共享，类似于 vue 中的 vuex，与Redux 相比，mobx 是极其简单的，他没有复杂的工作流程
    
    **特点：**
    
    - 无模版代码，非常简洁；
    - 数据是响应式的，可以直接修改数据(Proxy)；
    - 可以直接处理异步；
    - 适合简单、规模不大的应用
    
    **版本说明：**
    
    - Mobx4可以运行在任何支持ES5语法的浏览器；
    - Mobx5版本运行在任何支持ES6语法的浏览器；
    - Mobx4和Mobx5具有相同的api，都需要使用装饰器语法；
    - Mobx6是目前最新的版本，为了兼顾与标准JavaScript的最大兼容性，默认情况下放弃了装饰器语法。
    
    **mobx 和 redux 的区别：**
    
    工作流程：
    
    - Redux 要求必须严格遵守它的工作流程，例如通过 dispatch 触发 action，由 store 接收到 action，然后交给 reducer 去处理 action
    - MobX 没有过多的流程要求，直接调用定义的 action 方法修改状态，直接访问 Store 中的状态
    
    应用场景：
    
    - 项目团队：开发者的风格不同，如果团队中开发者比较多，推荐使用 Redux，因为 Redux 有严格的工作流程以及样板代码，从而可以约束每个人的代码风格。Redux 在多人或多个项目中共享状态比较方便
    - 个人开发：个人负责的项目或人数交少的，推荐使用 MobX，因为 MobX 代码简约无样板代码，相比 Redux 开发效率会高一些
- 安装步骤
    1. 安装依赖
        
        ```jsx
        yarn add mobx mobx-react 
        yarn add @babel/plugin-proposal-decorators
        ```
        
        @babel/plugin-proposal-decorators 使得 rn 项目支持 es7 的装饰器语法的库
        
    2. 在 babel.config.js 添加配置
        
        ```jsx
        plugins: [
            [
              "@babel/plugin-proposal-decorators", {'legacy': true}
            ]
          ]
        ```
        
    3. 
- 工作流程和原理
    
    ![Untitled](Untitled%2056.png)
    
    action：将一个方法标记为可修改 state 的 action
    
    observable state：定义一个存储 state 的可追踪字段（Proxy）
    
    computed value：标记一个可以由state派生出新值并且缓存其输出的计算属性
    
    ![Untitled](Untitled%2057.png)
    
    - 在视图中通过事件 event 触发 Action 方法
    - Action 方法用于更新（update）状态（Observable State）
    - 当状态（Observable State）发生变化，就会通知（notify）计算值（Computed Values）
    - 当计算值（Computed Values）同步完成完，就会触发（trigger）副作用（Side-effects），例如 render 更新视图
- 在类组件中使用
    1. 创建 store 来存放全局数据
    使用 @observable 和 @action 装饰器
        
        ```jsx
        import { observable, action } from "mobx";
        
        class RootStore {
                @observable name = "hello";
                @action.bound
                changeName(name) {
                        this.name = name;
                }
        }
        
        export default new RootStore();
        ```
        
    2. 在根组件 index 中来挂载
    <provider rootStore={rootStore}> </provider> 标签包裹
        
        ```jsx
        import React, { Component } from 'react';
        import { View } from 'react-native';
        import rootStore from "./mobx";
        import { Provider } from "mobx-react";
        
        class Index extend Component {
                render(){
                        <View>
                            <Provider rootStore={rootStore}>
                                <Sub1></Sub1>
                            </Provider>
                        </View>
                }
        }
        ```
        
    3. 在子组件中使用，监测数据变化
    @inject 和 @observer 装饰器挂在
    this.props.rootStore.name 来使用
        
        ```jsx
        import React, { Component } from 'react';
        import { View, Text } from 'react-native';
        import { inject, observer } from "mobx-react";
        
        @inject("rootStore")
        @observer
        class Sub1 extends Component {
                changeName = () => {
                        this.props.rootStore.changeName(Date.now());
                }
                render(){
                        console.log(this);
                        return() {
                                <View>
                                        <Text onPress={this.changeName}>{this.props.rootStore.name}</Text>
                                </View>
                        }
                }
        }
        ```
        
- 在函数式组件中使用
    1. 创建 store 来存放全局数据
    使用 makeObservable() 和 action.bound
        
        ```jsx
        import React from 'react';
        import { makeObservable, action, observable } from 'mobx';
        
        class CounterStore {
          count = 0;
        
          constructor() {
            makeObservable(this, {
              count: observable,
              increment: action.bound,
              decrement: action.bound,
                     reset: action,    // 如果要改数据，那么这个方法一定要标为action
              double: computed
            })
          }
        
          increment() {
            this.count += 1;
          }
        
          decrement() {
            this.count -= 1;
          }
        }
        export const CounterStoreContext = React.createContext( new CounterStore());
        ```
        
    2. 在其他子组件中使用，监测数据的变化
        - import observer 高阶组件函数
        - 使用 observer() 高阶组件函数包裹需要使用 store 的组件
        - import store 对象
        - 使用 store 对象的属性和方法即可
        
        ```jsx
        import { useObserver } from 'mobx-react';
        import CounterStore from './Counter.Store.js'
        const TestComponent = observer(() => {
            // use observable data
            return <div>{CounterStore.name}</div>
        });
        ```
        
- action 和 action.bound 的区别
    
    默认 class 中的方法不会绑定 this，this 指向取决于如何调用
    
    **示例一：action**
    
    ```jsx
    makeObservable(this, {
      count: observable,  // 属性是observable的
      increment: action,
      decrement: action,
      reset: action    // 如果要改数据，那么这个方法一定要标为action
    });
    ```
    
    ```jsx
    <button onClick={() => counter.increment()}>加1</button> // 正确
    <button onClick={counter.increment>加1</button> // 错误
    ```
    
    **示例二：action.bound**
    
    在使用makeObservable时可以通过action.bound绑定this指向
    
    ```jsx
    makeObservable(this, {
      count: observable,  // 属性是observable的
      increment: action.bound,
      decrement: action.bound,
      reset: action    // 如果要改数据，那么这个方法一定要标为action
    });
    ```
    
    ```jsx
    <button onClick={counter.increment}>加1</button>
    ```
    
- 计算属性的使用 computed
    
    computed 可以用来从其他可观察对象中派生信息。
    
    - 计算值采用惰性求值，会缓存其输出，并且只有当其依赖的可观察对象被改变时才会重新计算。
    - 计算属性是一个方法，且方法前面必须使用get进行修饰
    - 计算属性还需要通过 makeObservable 方法指定
    
    ```jsx
    get double() {
        return this.count * 2;
      }
    ```