---
wedrrrrrgbvvvvvvvvvvtitle: 设计模式二三事
date: 2022-03-26 12:27:31
tags: 
- Java
categories: 
- 学习
- Java

---



## 一、理解设计模式



### 理解设计模式

设计模式是软件开发人员经过长时间试错和应用总结出来的，解决特定问题的一系列方法。可以迅速提高代码的**可读性、健壮性、扩展性。**

参考链接：https://tech.meituan.com/2022/03/10/interesting-talk-about-design-patterns.html



> **策略模式**定义了一系列的算法，并将每一个算法封装起来，使它们可以相互替换。策略模式通常包含以下角色：1
>
> - 抽象策略（Strategy）类：定义了一个公共接口，各种不同的算法以不同的方式实现这个接口，环境角色使用这个接口调用不同的算法，一般使用接口或抽象类实现。
> - 具体策略（Concrete Strategy）类：实现了抽象策略定义的接口，提供具体的算法实现。
> - 环境（Context）类：持有一个策略类的引用，最终给客户端调用。



> **适配器模式**：将一个类的接口转换成客户希望的另外一个接口，使得原本由于接口不兼容而不能一起工作的那些类能一起工作。适配器模式包含以下主要角色：
>
> - 目标（Target）接口：当前系统业务所期待的接口，它可以是抽象类或接口。
> - 适配者（Adaptee）类：它是被访问和适配的现存组件库中的组件接口。
> - 适配器（Adapter）类：它是一个转换器，通过继承或引用适配者的对象，把适配者接口转换成目标接口，让客户按目标接口的格式访问适配者。



> **单例模式**：设计模式属于创建型模式，它提供了一种创建对象的最佳方式。
>
> - 这种模式涉及到一个单一的类，该类负责创建自己的对象，
> - 同时确保只有单个对象被创建。
> - 这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。



### 七大基本原则（SOLID）：

1. 单一职责原则 (Single Responsibility Principle)
2. 开放-关闭原则 (Open-Closed Principle)
3. 里氏替换原则 (Liskov Substitution Principle)
4. 依赖倒转原则 (Dependence Inversion Principle)
5. 接口隔离原则 (Interface Segregation Principle)
6. 迪米特法则（Law Of Demeter）
7. 组合/聚合复用原则 (Composite/Aggregate Reuse Principle)

参考链接： https://zhuanlan.zhihu.com/p/24614363



### 1.单例模式

单例模式（Singleton Pattern）是 Java 中最简单的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

**注意：**

- 1、单例类只能有一个实例。

- 2、单例类必须自己创建自己的唯一实例。

- 3、单例类必须给所有其他对象提供这一实例。

  

**懒汉式(线程不安全)：**

```java
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
  
    public static Singleton getInstance() {  
        if (instance == null) {  
            instance = new Singleton();  
        }  
        return instance;  
    }  
```

**懒汉式(线程安全)**：

```java
public class Singleton{
	private static final instance;
	private Singleton(){};
	public static synchronized Singleton getInstance(){
	 	if(instance == null){
	 		instance = new Singleton();
	 	}
	 	return instance;
	}
}
```

**饿汉式(线程不安全):**

```
public class Singleton{
	private static final instance = new Singleton();
	private singleton(){};
	public static Singleton getInstance(){
		return instance;
	}
}
```

**双检锁/双重校验锁（DCL，即 double-checked locking）**

```java
public class Singleton{
    private volatile static instance;
    private Singleton(){};
    public static Singleton getInstance(){
        if(instance == null){
            synchronize(Singleton.class){
                instance = new Singleton();
            }
        }
        return instance;
    }
}
```

### 2.代理模式

### 3.观察者模式

### 4.工厂模式





<!-- more -->