---
title: JVM学习
date: 2020-08-16 14:05:37
tags: [JVM]  
categories: 学习
---

JVM学习记录

<!--more-->

# JVM复习点

## 1.编译器

java->class

scala groovy

jvm工作流程：类加载+JMM



## 2.类加载过程

### 2.1 类的生命周期

**加载**

​		加载class文件的信息加载到内存中，由硬盘到内存的迁移。

**链接**

​		将加载阶段加载到内存中的二进制数据整合到虚拟机中。

​		**验证**

​					文件格式验证

​					元数据验证等（语法、关键字）

​		**准备**

​					为类静态变量分配内存，并将其初始化为*<u>默认值</u>*

​					给常量分配内存并*<u>设置常量值</u>*

​		**解析**

​					把类型中的符号引用转换为内存引用

**初始化**

​		执行类的构造器（静态变量、静态代码块），为类的静态变量赋予正确的初始化值按照**<u>*从上到下*</u>**的顺序（<clint>）

**使用**

​		实例化对象（<init>）

**卸载**

​		类使用完、不再使用时，卸载类（必须保证所有实例都被GC）



总结：

1.静态变量设置默认值、常量设置指定值；

2.静态变量从上到下设置初始化值

3.实例化对象



### 2.2 clinit和init

**clinit：**

​		类静态变量初始化

​		类静态语句块

**init：**

​		类变量初始化和类语句快

​		构造函数

创建类实例时，先调用clinit再调用init



### 2.3 代码实例（类加载过程）

```java
class SingleTone{
    /*1.准备：为类的静态变量设置默认值 singleTone=null count1=0 count2=0
     *2.初始化：singleTone = new SingleTone() count1=1，count2=2
     */
    private static SingleTone singleTone = new SingleTone();
    public static int count1;   //3.未赋值，仍为1
    public static int count2=0; //4.重新赋值0

    private SingleTone(){
        count1++;
        count2++;
    }

    public static SingleTone getSingleTone() {
        return singleTone;
    }
}

public class ClaaLoaderTest {
    public static void main(String[] args) {
        SingleTone singleTone = SingleTone.getSingleTone();
        System.out.println(singleTone.count1);
        System.out.println(singleTone.count2);
        //输出：1，0
    }
}
```



### 2.4 类加载过程

方法区：用于存储虚拟机加载类的信息、常量、静态变量，是各个线程贡献的内存区域。

程序计数器：当前线程所执行的字节码的行号指示器。

虚拟机栈：属于线程私有，“栈帧”用于存储局部变量表（包含参数）、操作栈、方法出口等信息。变量的引用也放在栈里。

堆：被各个线程共享的内存，用来存放对象。



每个方法对应一个栈帧（执行对应着栈帧的入栈和出栈），栈帧中存有变量表（属于线程私有，是线程安全的）。如果执行方法过多（递归）会造成内存溢出（StackOverflowError，OOM的一种）



## 3.JMM（java内存模型）

<img src="/Users/vic/Documents/study/workspace/Vvvvvvvvvvvvvvvvicky.github.io/source/_posts/JVM学习/编译.jpg" alt="编译" style="zoom:50%;" />



## 4.程序中方法执行的内存语意

栈帧的入栈和出栈

栈溢出原理



## 5.栈溢出



## 6.new指令分配堆内存的方式

（1）指针碰撞

线程安全问题的解决：①加锁；②TLAB每个线程创建时分配一定大小的内存区域。使用volatile关键字实现现场间变量的可见性。

（2）空闲列表



## 7.内存角度分析程序执行

程序代码实例

```java
package club.vic.designPatternPractice;

/*
 * 1.编译：java->.class文件
 * 2.类加载：加载到虚拟机
 */

//7：方法区：类结构
class Test{
    //8。方法区：name是哥引用，放在对应的栈中。
    private String name;
    //9。执行类实例化
    public Test(String name){
        this.name = name;
    }
    //11。方法信息存储在方法区
    public void printName(){
        System.out.println("name is "+this.name);
    }
}

/*
 * 3。方法区：类结构
 */
public class AppMain {
    //4。方法区：方法的结构（含参数）
    //5。main方法对应的线帧，对于主线程来讲为入栈  args存储在局部变量表中
    public static void main(String[] args) {
        //6。使用Test类时发现此时还没有加载该类 引用都放在栈里
        Test test = new Test("张三");
        //10。主线程的printName方法入栈
        test.printName();
        //12。主线程的printName方法出栈
    }
}
//13。主线程的main方法入栈
	
```



## 8.ClassLoader

1.JVM运行流程、JVM基本结构

<img src="/Users/vic/Documents/study/workspace/Vvvvvvvvvvvvvvvvicky.github.io/source/_posts/JVM学习/JVM运行流程.jpg" alt="JVM运行流程" style="zoom:50%;" />

JVM基本结构

​	类加载器、执行引擎、运行时数据区（堆、栈、方法区、本地方法栈、虚拟机栈）、本地接口

Class Files -> ClassLoader -> 运行时数据区 -> 执行引擎，本地库接口 -> 本地方法库



类的装载：

​	***<u>加载</u>***、链接（验证、准备、解析）、初始化、使用、卸载

2.类加载器的双亲委派模式

3.ClassLoader源码分析

4.实现自定义的类加载器