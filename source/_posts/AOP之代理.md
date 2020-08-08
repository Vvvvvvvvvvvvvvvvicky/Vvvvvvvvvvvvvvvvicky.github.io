---
title: AOP之代理
date: 2019-10-10 11:01:24
tags: 代理  
categories: 学习  
comments: true  
---



各种代理的学习

<!--more-->

无代理：直接在方法内部修改

静态代理：新建一个类，调用原有类，在其前后增加补充操作

JDK动态代理：继承InvocationHandler，实现invoke方法，通过反射实现

CGLib动态代理：继承MethodInterceptor，实现intercept方法，提供方法级别的代理（可以代理没有任何接口的类）



原理区别：

java动态代理是利用反射机制生成一个实现代理接口的匿名类，在调用具体方法前调用InvokeHandler来处理。

而cglib动态代理是利用asm开源包，对代理对象类的class文件加载进来，通过修改其字节码生成子类来处理。

1、如果目标对象实现了接口，默认情况下会采用JDK的动态代理实现AOP 
2、如果目标对象实现了接口，可以强制使用CGLIB实现AOP 

3、如果目标对象没有实现了接口，必须采用CGLIB库，spring会自动在JDK动态代理和CGLIB之间转换



JDK动态代理和CGLIB字节码生成的区别？
 （1）JDK动态代理只能对实现了接口的类生成代理，而不能针对类
 （2）CGLIB是针对类实现代理，主要是对指定的类生成一个子类，覆盖其中的方法
   因为是继承，所以该类或方法最好不要声明成final 



ref：https://www.cnblogs.com/leifei/p/8263448.html [Spring的两种动态代理：Jdk和Cglib 的区别和实现]