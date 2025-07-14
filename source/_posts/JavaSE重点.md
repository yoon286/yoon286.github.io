---
title: JavaSE重点
date: 2021-04-14 23:19:50
tags: 
- Java
- 基础语法
categories: 
- 学习
- Java
---

##### 1.error 和 exception 有啥区别

##### 2.hash 扩容

<!-- more -->

-----



##### 3.Java 和 JavaScript 有啥区别

> http://www.ruanyifeng.com/blog/2011/06/birth_of_javascript.html

+ 它们的相同之处包括：
  + 它们的语法和 C 语言都很相似；
  + 它们都是面向对象的（虽然实现的方式略有不同）；
  + JavaScript 在设计时参照了 Java 的命名规则；   

+ 它们的不同之处包括：
  +  JavaScript 是动态类型语言，而 Java 是静态类型语言；
  + JavaScript 是弱类型的，Java 属于强类型；
  + JavaScript 的面向对象是基于原型的（prototype-based）实现的，Java 是基于类（class-based）的；

---



##### 4.final，finally，finalized 的区别



##### 5.final的特点及应用

final可以修饰类/方法/局部变量/成员变量

+ 对于类来说：如果用final修饰，则当前类不能有任何子类，那么其中的所有成员方法都不能覆盖重写

+ 对于方法来说：当用final来修饰方法时，则该方法是最终方法。

> 注意：对于类与方法来说，abstract与final不能同时使用。

+ 对于局部变量来说：一次赋值，终身不变。同时，对于基本数据类型来说，不可变说的是数据不变。对于引用类型来说，不可变说的是地址值不变。
+  对于成员变量来说：一定要进行手动赋值，要么通过构造方法赋值，要么直接赋值。

---



##### 6.修饰符使用范围

| 关键字 | private         | default         | protected         | public              |
| ------ | --------------- | --------------- | ----------------- | ------------------- |
|        | 本类当中/我自己 | 同一个包/我邻居 | 不同包子类/我儿子 | 不同包不同类/陌生人 |
|        |                 |                 |                   |                     |
|        |                 |                 |                   |                     |

