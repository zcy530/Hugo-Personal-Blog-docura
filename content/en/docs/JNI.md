---
title: Java Native Interface
slug: Java-Native-Interface
lastmod: 2025-07-01T00:00:00+00:00
---


# JNI usage

## 介绍和作用

JNI 是 Java Native Interface，作用是让 Java 和 C/C++ 之间可以互相调用对方的函数，因为Java是运行在 JVM 上的，而 C/C++ 是本地语言（Native），它们本身不能直接通信，所以需要 JNI 这个中介

## 为什么Java需要调用C++函数

1. 复用已有的 C/C++ 库
    
    比如你已经有个很牛的图像处理库是用 C++ 写的，现在想在 Android App（Java/Kotlin 写的）里用它，就得用 JNI
    
2. 性能要求高的部分用 C/C++ 实现
    
    比如视频编解码、图像滤镜这种对速度要求特别高的模块，Java 跑得慢，所以用 C++
    
3. 调用系统底层接口
    
    比如 Android 上一些底层系统功能只能用 Native 层的 API，Java 访问不到，只能通过 JNI 间接访问
    

## 为什么C++需要回调Java函数

1. 当 Java 需要执行一个 C++ 函数时，Java 会调用一个 native 方法
2. 而当过程中 C++ 执行一些任务时，它需要访问 Java 的功能（比如 log 方法），这就必须通过 JNI 来实现。因此，C++ 通过 JNI 来间接调用 Java 方法

## 从Java调用C++函数的流程

首先在 java 端定义 native 函数

```cpp
// MyClass.java
public class MyClass {
    static {
        System.loadLibrary("native-lib"); // 加载 native 库
    }

    public native int add(int a, int b); // 声明 native 方法

    public static void main(String[] args) {
        MyClass obj = new MyClass();
        int result = obj.add(3, 4);
        System.out.println("Result from C++: " + result);
    }
}
```

实现这个 add 函数的 C++ 版本

```cpp
// C++ 代码（native-lib.cpp）
#include <jni.h>

extern "C"
JNIEXPORT jint JNICALL
Java_MyClass_add(JNIEnv *env, jobject obj, jint a, jint b) {
    return a + b;
}
```

## 从C++调用Java函数的流程

现在我们让 C++ 反过来调用 Java 中的 printLog(String) 方法

比如你有一个 Java 类，里面有个方法是打印日志的

```cpp
// Logger.java
public class Logger {
    public void printLog(String msg) {
        System.out.println("Java log: " + msg);
    }
}
```

你在 C++ 中想调用这个 Java 方法，就要用到 GetObjectClass() 和 GetMethodID()

```cpp
#include <jni.h>

extern "C"
JNIEXPORT void JNICALL
Java_MyClass_callLogger(JNIEnv *env, jobject thiz, jobject loggerObj) {
    // 获取 loggerObj 的类，创建了 local reference（1）
    jclass loggerClass = env->GetObjectClass(loggerObj);

    // 获取 printLog(String) 方法 ID
    jmethodID logMethod = env->GetMethodID(loggerClass, "printLog", "(Ljava/lang/String;)V");

    // 创建 Java 字符串作为参数，创建了 local reference（2）
    jstring msg = env->NewStringUTF("Hello from C++");

    // 调用 Java 方法：logger.printLog("Hello from C++")
    env->CallVoidMethod(loggerObj, logMethod, msg);

    // 清理局部引用（好习惯）
    env->DeleteLocalRef(loggerClass);
    env->DeleteLocalRef(msg);
}

```

最后，使用java来调用这个 JNI 函数，注意 JNI 的工作方式是 C++ 通过 Java 提供的接口调用 Java 方法，但是 C++ 不能直接运行 Java 方法，所以还需要写一个类来调用这个 native 函数作为入口

```cpp
public class MyClass {
    static {
        System.loadLibrary("native-lib");
    }

    public native void callLogger(Logger logger);  // 声明 native 方法

    public static void main(String[] args) {
        Logger logger = new Logger();
        MyClass obj = new MyClass();
        obj.callLogger(logger);  // 这里调用了 native 方法
    }
}
```

## JNIEnv* env 和 jobject

JNIEnv* env 是 JNI 的“上下文”，你用它来访问 Java 世界，比如调用 Java 方法、创建对象等等。jobject obj 是 MyClass 的实例，相当于 Java 中的 this，你可以通过它访问成员变量、方法

## JNI Local Reference

每次你在 C++ 里通过 env->NewObject()、env->GetObjectClass() 创建了一个 Java 对象或类引用，它就是一个 local reference

哪些 JNI 方法会创建 local reference

| 类别 | 方法 | 创建 LocalRef 吗？ | 说明 |
| --- | --- | --- | --- |
| 类/方法查找 | FindClass | ✅ 是 | 返回 jclass，是 local ref |
|  | GetMethodID / GetStaticMethodID | ❌ 否 | 返回 ID，不是引用 |
|  | GetFieldID / GetStaticFieldID | ❌ 否 | 返回 ID，不是引用 |
| 数组操作 | NewObjectArray / NewBooleanArray
NewByteArray / NewCharArray | ✅ 是 | 创建数组对象，是 local ref |
|  | GetObjectArrayElement | ✅ 是 | 每次返回数组里的元素 |
|  | SetObjectArrayElement | ❌ 否 | 只赋值，不返回引用 |
|  | GetArrayLength | ❌ 否 | 只返回长度，不产生引用 |
| 对象操作 | NewObject | ✅ 是 | 返回实例，是 local ref |
|  | GetObjectClass | ✅ 是 | 返回 jclass，是 local ref |
|  | GetSuperclass | ✅ 是 | 返回 jclass，是 local ref |
|  | IsInstanceOf | ❌ 否 | 返回 jboolean，不是引用 |
| 调用方法 | CallObjectMethod | ✅ 是 | 返回对象，是 local ref |
|  | CallStaticObjectMethod | ✅ 是 | 返回对象，是 local ref |
|  | Call<Type>Method
(Type是Int/Float等基本类型) | ❌ 否 | 基本类型不产生引用 |
|  | CallStatic<Type>Method(Type是Int/Float等基本类型) | ❌ 否 | 基本类型不产生引用 |
| 异常处理 | ExceptionOccurred | ✅ 是 | 返回异常对象，是 local ref |
|  | ExceptionClear / ExceptionDescribe | ❌ 否 | 只操作，不返回对象 |
| 字符串操作 | NewString / NewStringUTF | ✅ 是 | 返回字符串对象，是 local ref |
|  | GetStringChars / GetStringUTFChars | ❌ 否 | 返回原始指针，不是引用 |
|  | ReleaseStringChars / ReleaseStringUTFChars | ❌ 否 | 释放原始指针 |
|  | GetStringLength / GetStringUTFLength | ❌ 否 | 返回长度，不产生引用 |
| 引用管理 | NewLocalRef | ✅ 是 | 明确创建一个新的 local ref |
|  | DeleteLocalRef | ❌ 否 | 删除引用，不产生引用 |
|  | NewGlobalRef | ✅ 是 | 不是 LocalRef，但要注意内存 |
|  | DeleteGlobalRef | ❌ 否 | 删除 GlobalRef |
|  | NewWeakGlobalRef | ✅ 是 | 不是 LocalRef，但需要管理 |
|  | DeleteWeakGlobalRef | ❌ 否 | 删除 WeakGlobalRef |
| 线程管理 | AttachCurrentThread / DetachCurrentThread | ❌ 否 | 和 local ref 无关 |
|  | GetEnv | ❌ 否 | 获取 JNIEnv 指针，不涉及引用 |
| 其他 | MonitorEnter / MonitorExit | ❌ 否 | 线程同步，不产生引用 |
|  | PushLocalFrame / PopLocalFrame | ❌ 否 | 手动管理 local ref 容量，自己不产生引用 |