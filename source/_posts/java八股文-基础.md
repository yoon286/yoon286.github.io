---
title: 基础语法
date: 2022-01-19 23:27:31
tags: 
- Java
categories: 
- 学习
- Java
---



## 一、基础语法

### 1.面向对象包括哪些特性，如何理解？

- 封装。通过private关键字，将对象的属性和方法封装起来。隐藏一切可隐藏的东西，只对外界提供最简单的编程接口，同时保护了数据。

- 继承。父类引用指向子类对象，Animal animal = new Cat( ) 即声明的是父类，实际指向的是子类的一个对象。 继承是为了重用父类代码，子类继承父类就拥有了父类的成员。

- 多态。同一个行为具有不同的表现形式。实现多态需要做两件事：

  第一：方法重写（子类继承父类并重写父类中已有的或抽象的方法）

  第二：对象造型（用父类引用指向子类对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。

  <!-- more -->

### 2.重载和重写的区别

**重载** : 发生在同一个类中。方法名一样，方法参数类型、个数、顺序不一样。返回值类型和访问权限可以不一致。

**重写** ：发生在父子类中，子类重写父类方法。方法名一样，方法返回值小于等于父类，方法访问权限大于等于父类。当父类中方法使用private修饰时，子类不能重写父类中的方法。

### 3.String、StringBuffer、StingBuilder的区别

- **可变性**

  String类中使用final关键字字符数组保存字符串，所以String是不可变字符串。

  StringBuilder和StringBuffer都继承自AbstractStringBuilder，因此两者都是可变字符串

- **线程安全性**

  String可以理解为字符串常量，因此是线程安全的。

  StringBuffer对方法或者调用的方法加了同步锁，因此也是线程安全的。

  StringBuilder并没有对方法加同步锁，所以是非线程安全的。

- **性能**

  String每次都会创建一个新的对象，并将指针指向这个新对象。

  StringBuffer每次都是对对象本身进行操作，相同情况下，StringBuilder比StringBuffer的性能提升10%-15%，却要承担线程不安全的风险

- 使用总结：

  对字符串进行少量修改：使用String

  多线程操作字符串缓冲区下操作大量数据：StringBuffer

  单线程操作字符串缓冲区下操作大量数据：StringBuilder



### 4.自动装箱与自动拆箱

自动装箱：将基本数据类型用他们对应的包装数据类型包装起来

自动拆箱：将包装数据类型转化为基本数据类型

> 在通过valueOf方法创建Integer对象的时候，如果数值在[-128,127]之间，便返回指向IntegerCache.cache中已经存在的对象的引用；否则创建一个新的Integer对象。



### 5.关于final关键字的总结

final关键字主要用在三个地方：类、方法、变量。

- 当final修饰变量时，一旦变量被初始化，就不可以被随意更改。
- 当final修饰方法时，这个方法不可以被覆盖重写。
- 当final修饰类时，该类不可以被继承，类中的方法被隐式地申明为final方法。

使用final类的好处如下：第一是把方法锁住，防止继承类修改它的含义；第二是提升性能，在早期的Java版本中，final方法会转化为嵌入方法，不过现在的Java版本已经不靠final来提升方法性能了。



### 6.Object类的常用方法总结

Object类是一个特殊的类，它是所有类的父类，主要提供了以下几个方法：

```java
- toString() 
    
- hashCode()
    
- getClass() //native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。
    
- equals() //用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。
    
- clone() //naitive方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass()== x.getClass() 为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。
    
- notify() //native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。

- notifyAll() //native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。

- wait() //native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。

- finalize() //实例被垃圾回收器回收的时候触发的操作     

```



### 7.Java中的异常处理

#### 7.1 异常分类

在Java中所有的异常都有一个共同的父类**Throwable**类，Throwable类有两个重要的子类：**Error **和 **Exception**。

Error是程序无法处理的异常，Exception是程序可以处理的异常。

![image-20220319231142003](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202203192311254.png)

#### 7.2 异常处理

处理方式：

1. 不处理，直接抛出异常
2. 使用 try catch 捕获处理异常

#### 7.3 throw throws区别

##### 位置不同：

throws: 使用在函数上，后面跟的是异常类，可以跟多个

throw: 使用用在方法内，后面跟的是异常对象，只能跟一个

##### 功能不同：

throws: 申明可能抛出的异常，不一定发生，可以进行预处理

throw: 功能执行到此结束，将具体异常对象抛给调用者



### 8.接口和抽象类的区别是什么

1. 接口类的变量必须是final类型，抽象类不一定

2. 接口类的方法默认加了public abstract JDK1.8之后接口类可以具有默认的实现方法

   抽象类中可以有非抽象的方法

3. 子类可以继承一个或多个接口，却只能继承一个抽象方法

4. 继承了接口的子类必须实现接口的所有抽象方法，继承了抽象类的子类可以不完全实现，但是不完全实现的子类也会自动转换为抽象类



### 9.反射

在 Java 中的反射机制是指**在运行状态中，对于任意一个类都能够知道这个类所有的属性和方法； 并且对于任意一个对象，都能够调用它的任意一个方法**；这种动态获取信息以及动态调用对象方法的功能成为 Java 语言的反射机制。

#### 9.1 编译时类型和运行时类型

>  Person p = new Student （）；

编译时类型为Person，运行时类型为Student，当程序需要获取运行时的对象属性和方法时，需要用到反射机制

#### 9.2 反射API

class 类：反射的核心类，用来获取对象的属性和方法等

field 类：反射的基本类，用来表示对象的变量，可以用来获取和修改属性值

method 类：反射的基本类，用来获取对象的方法

 constructor 类：java . lang . reflect 类中方法，表示类的构造方法

#### 9.3 获取对象的三种方法

**调用某个对象的 getClass() 方法**

> Person p = new Person();
>
> Class clazz = p.getClass();

**调用某个类的 class 属性**

> Class clazz = Person.Class;

**使用forName()方法**

> Class clazz = Class.forName("类的全限定名称");  //最常用的方法

#### 9.4 操作反射相关的API

```java
//获取 Person 类的 Class 对象
 Class clazz=Class.forName("reflection.Person");

//获取 Person 类的所有方法信息
 Method[] method=clazz.getDeclaredMethods();
 
//获取 Person 类的所有成员属性信息
 Field[] field=clazz.getDeclaredFields();

//获取 Person 类的所有构造方法信息
 Constructor[] constructor=clazz.getDeclaredConstructors();
```



### 10.注解

**Annatation**(注解)是一个接口，程序可以通过反射来获取指定程序中元素的 Annotation 对象，然后通过该 Annotation 对象来获取注解中的元数据信息。

**@Target 修饰的对象范围** 

@Target说明了Annotation所修饰的对象范围： Annotation可被用于 packages、types（类、 接口、枚举、Annotation 类型）、类型成员（方法、构造方法、成员变量、枚举值）、方法参数 和本地变量（如循环变量、catch 参数）。在 Annotation 类型的声明中使用了 target 可更加明晰 其修饰的目标 



**@Retention 定义 被保留的时间长短** 

Retention 定义了该 Annotation 被保留的时间长短：表示需要在什么级别保存注解信息，用于描 述注解的生命周期（即：被描述的注解在什么范围内有效），取值（RetentionPoicy）由：  SOURCE:在源文件中有效（即源文件保留）  CLASS:在 class 文件中有效（即 class 保留）  RUNTIME:在运行时有效（即运行时保留） 

**@Documented 描述-javadoc**



**@ Documented 用于描述其它类型的 annotation** 应该被作为被标注的程序成员的公共 API，



### 11.浅拷贝与深拷贝

**浅拷贝**：对基本数据类型进行**值传递**，对引用数据类型进行**引用传递**

**深拷贝**：对基本数据类型进行**值传递**，对引用数据类型，创建一个新的对象，并复制其内容

对 clone() 方法，只能对当前对象进行浅拷贝，引用类型依然是在传递引用。

那么，如何进行一个深拷贝呢？

比较常用的方案有两种：

1. 序列化（serialization）这个对象，再反序列化回来，就可以得到这个新的对象，无非就是序列化的规则需要我们自己来写。
2. 继续利用 clone() 方法，既然 clone() 方法，是我们来重写的，实际上我们可以对其内的引用类型的变量，再进行一次 clone()。





## 二、集合框架

### **1.List集合**

 **ArrayList ：** 数据结构底层是 Object 数组。扩容时，需要将已有数组的数据复制到新的存储空间中。适合随机查找和遍历，不适合插入和删除。

**Vector ：** 数据结构底层是 Object 数组。支持线程的同步。<font color = #bbbb>即某一时刻只有一 个线程能够写 Vector，避免多线程同时写而引起的不一致性，</font>但实现同步需要很高的花费，因此， 访问它比访问 ArrayList 慢。

**LinkedList ：**数据结构底层是双向链表。很适合数据的动态插入和删除，随机访问和遍历速度比较 慢。另外，他还提供了 List 接口中没有定义的方法，专门用于操作表头和表尾元素，可以当作堆、栈、队列和双向队列使用。



### 2.Set集合

**HashSet ：** <font color=#bbbb>存储元素的顺序并不是按照存入时的顺序（和 List 显然不 同）</font> 而是按照哈希值来存的所以取数据也是按照哈希值取得。元素的哈希值是通过元素的 hashcode 方法来获取的, HashSet 首先判断两个元素的哈希值，如果哈希值一样，接着会比较 equals 方法。



**TreeSet：** 

1. TreeSet()是使用二叉树的原理对新 add()的对象按照指定的顺序排序（升序、降序），每增 加一个对象都会进行排序，将对象插入的二叉树指定的位置。 

2. Integer 和 String 对象都可以进行默认的 TreeSet 排序，而自定义类的对象是不可以的，<font color=#bbbb>自定义的类必须实现 Comparable 接口，并且重写相应的 compareTo()函数，</font>才可以正常使 用。 

3.  在覆写 compareTo()函数时，要返回相应的值才能使 TreeSet 按照一定的规则来排序 

4. 比较此对象与指定对象的顺序。如果该对象小于、等于或大于指定对象，则分别返回负整 数、零或正整数。

   

**LinkedHashSet：** 底层使用 LinkedHashMap 来保存所有元素，它继承与 HashSet，其所有的方法 操作上又与 HashSet 相同，因此 LinkedHashSet 的实现上非常简单，只提供了四个构造方法，并 通过传递一个标识参数，调用父类的构造器，底层构造一个 LinkedHashMap 来实现，在相关操 作上与父类 HashSet 的操作相同，直接调用父类 HashSet 的方法即可



### **3.Map集合**

#### 1. HashMap 和 Hashtable 的区别

1. **线程是否安全：** HashMap 是非线程安全的，HashTable 是线程安全的；HashTable 内部的方法基本都经过 synchronized 修饰。（要保证线程安全的话就使用 ConcurrentHashMap 吧！）； 

2. **效率：** 因为线程安全的问题，HashMap 要比 HashTable 效率高一点。另外，HashTable 基本被淘汰，不要在 代码中使用它； 

3. **对Null key 和Null value的支持：** HashMap 中，null 可以作为键，这样的键只有一个，可以有一个或多个键 所对应的值为 null。。但是在 HashTable 中 put 进的键值只要有一个 null，直接抛出 NullPointerException。 

4. **初始容量大小和每次扩充容量大小的不同 ：**

    ①创建时如果不指定容量初始值，Hashtable 默认的初始大小为 11，之后每次扩充，容量变为原来的2n+1。HashMap 默认的初始化大小为16。之后每次扩充，容量变为原来 的2倍。

   ②创建时如果给定了容量初始值，那么 Hashtable 会直接使用你给定的大小，而 HashMap 会将其扩充 为2的幂次方大小。也就是说 HashMap 总 是使用2的幂作为哈希表的大小,后面会介绍到为什么是2的幂次方。

5.  **底层数据结构：** JDK1.8 以后的 HashMap 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）时，将链表转化为红黑树，以减少搜索时间。Hashtable 没有这样的机制。

#### 2.ConcurrentHashMap 和 Hashtable 的区别

ConcurrentHashMap 和 Hashtable 的区别主要体现在实现线程安全的方式上不同。 

- **底层数据结构：**ConcurrentHashMap 数组+链表/红黑二叉树。Hashtable 采用 数组+链表 的形式

- **实现线程安全的方式（重要）：**

  ① ConcurrentHashMap 使用 Node 数组+链表+红黑 树的数据结构来实现，并发控制使用 synchronized 和 CAS 来操作。

  ② Hashtable(同一把锁) :使用 synchronized 来保证线程安全， 效率非常低下。当一个线程访问同步方法时，其他线程也访问同步方法，可能会进入阻塞或轮询状态，如使用添加元素，另一个线程不能使用 put 添加元素，也不能使用 get，竞争会越来越激烈效率越低。



#### 3.Map数据结构总结

**HashMap：**数组+链表/红黑树，

**LinkedHashMap:**  继承自 HashMap，数组+链表/红黑树。另外，LinkedHashMap 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。

**HashTable:** 数组+链表组成的，

**TreeMap:** 红黑树（自平衡的排序二叉树）



#### 4.HashMap扩容机制

**当前存放新值（*注意不是替换已有元素位置时*）的时候已有元素的个数大于等于阈值（已有元素等于阈值，下一个存放后必然触发扩容机制）**

　　注：

　　（1）扩容一定是放入新值的时候，该新值不是替换以前位置的情况下（说明：put（“name”,"zhangsan"），而map里面原有数据<"name","lisi">，则该存放过程就是替换一个原有值，而不是新增值，则不会扩容）

　　（2）扩容发生在存放后，即是数据存放后（先存放后扩容），判断当前存入对象的个数，如果大于阈值则进行扩容。



## 三、多线程

### 1.多线程的创建方式

#### 继承 Thread 类

1) 定义子类继承Thread类。

2) 子类中重写Thread类中的run方法。

```java
public class MyThread extends Thread{

	@Override
	public void run(){
	
	}
};
```

 3) 创建Thread子类对象，即创建了线程对象。 

```java
MyThread mt = new MyThread();
```

4) 调用线程对象start方法：启动线程，调用run方法。

```java
mt.start();
```

 注意点：

1.  如果自己**手动调**用run()方法，那么就只是**普通方法，没有启动多线程模式**。
2.   run()方法由JVM调用，什么时候调用，执行的过程控制都有操作系统的CPU 调度决定
3.  想要启动多线程，必须调用start方法。 
4.  一个线程对象只能调用一次start()方法启动，如果重复调用了，则将抛出以上 的异常“IllegalThreadStateException”。



#### 实现 runnable 、callable 接口

1) 定义子类，实现Runnable接口。

2) 子类中重写Runnable接口中的run方法。

```java
public class TestRunnable implements Runnable{
	@Override
	public void run(){};
}
```

3) **通过Thread类含参构造器创建线程对象。** 

4) 将Runnable接口的子类对象作为实际参数传递给Thread类的构造器中。 

5) 调用Thread类的start方法：开启线程，调用Runnable子类接口的run方法。

```java
TestRunnable test = new TestRunnable();
//含参构造器,开启线程
Thread(test."threadName").start();
```



##### ** 通过实现方式创建线程的好处 **

​		避免了单继承的局限性 

​		多个线程可以共享同一个接口实现类的对象，非常适合多个相同线 程来处理同一份资源。



##### ** runnable和callable的区别 **

与使用Runnable相比， Callable功能更强大些 

- 相比run()方法，可以借助FutureTask类，比如获取返回结果

- 方法可以抛出异常 

- 支持泛型的返回值 

```java
//通过实现callable创建线程
public class MyCallable implements Callable<String> {
    @Override
    public String call() {}
}

public static void main(String[] args) {
        // 1.创建callable对象
        Callable<String> myCallable = new MyCallable();
        // 2.由上面的callable对象创建一个FutureTask对象
        FutureTask<String> oneTask = new FutureTask<String>(myCallable);
        // 3.由FutureTask创建一个Thread对象
        Thread t = new Thread(oneTask);
        // 4.开启线程
        t.start();
}
```



#### 创建线程池

 背景：**经常创建和销毁、使用**量特别大的资源，比如并发情况下的线程， **对性能影响很大**。 

 思路：提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中。可以避免频繁创建销毁、实现重复利用。

 好处： 

​		 提高响应速度（减少了创建新线程的时间） 

​		 降低资源消耗（重复利用线程池中线程，不需要每次都创建） 

​		 便于线程管理 ，参数如下：

​				 corePoolSize：核心池的大小 

​				 maximumPoolSize：最大线程数 

​				 keepAliveTime：线程没有任务时最多保持多长时间后会终止



### 2.线程池的创建方式

java中提供了线程池创建的**顶级接口：ExcutorService**。ThreadPoolExcutor实现了ExcutorService，Excutors创建线程池返回一个ExcutorService对象。

https://tech.meituan.com/2020/04/02/java-pooling-pratice-in-meituan.html



> 【强制要求】线程池不允许使用 Executors 去创建，而是通过 ThreadPoolExecutor 的方式，这样的处理方式让写的同学更加明确线程池的运行规则，规避资源耗尽的风险。
>
> 说明：Executors 返回的线程池对象的弊端如下：
>
> 1） FixedThreadPool 和 SingleThreadPool：允许的请求队列长度为 Integer.MAX_VALUE，可能会堆积大量的请求，从而导致 OOM。
>
> 2）CachedThreadPool：允许的创建线程数量为 Integer.MAX_VALUE，可能会创建大量的线程，从而导致 OOM。



##### ** 通过 ThreadPoolExcutor 创建**

​	最原始的创建线程池的方式，它包含了 7 个参数可供设置。

```java
 public ThreadPoolExecutor(int corePoolSize,//核心线程数，线程池中始终存活的线程数。
                           int maximumPoolSize,//最大线程数
                           long keepAliveTime,//最大线程存活时间
                           TimeUnit unit,//最大线程存活时间单位
                           BlockingQueue<Runnable> workQueue,//阻塞队列，用来存储线程池等待执行的任务
                           ThreadFactory threadFactory,//线程工厂，主要用来创建线程，默认为正常优先级、非守护线程
                           RejectedExecutionHandler handler//拒绝策略，拒绝处理任务时的策略，系统提供了 4 种可选
                          ) {
     // 省略...
 }
```

使用实例：

```java
public static void myThreadPoolExecutor() {
    // 创建线程池
    ThreadPoolExecutor threadPool = new ThreadPoolExecutor(5, 10, 100, 													TimeUnit.SECONDS, new LinkedBlockingQueue<>(10));
    // 执行任务
    for (int i = 0; i < 10; i++) {
        final int index = i;
        threadPool.execute(() -> {
            System.out.println(index + " 被执行,线程名:" + 						 											Thread.currentThread().getName());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
    }
}

```



##### ** 通过 Excutors 创建**

1. Executors.newFixedThreadPool：创建一个固定大小的线程池，可控制并发的线程数，超出的线程会在队列中等待；
2. Executors.newCachedThreadPool：创建一个可缓存的线程池，若线程数超过处理所需，缓存一段时间后会回收，若线程数不够，则新建线程；
3. Executors.newSingleThreadExecutor：创建单个线程数的线程池，它可以保证先进先出的执行顺序；
4. Executors.newScheduledThreadPool：创建一个可以执行延迟任务的线程池；
5. Executors.newSingleThreadScheduledExecutor：创建一个单线程的可以执行延迟任务的线程池；
6. Executors.newWorkStealingPool：创建一个抢占式执行的线程池（任务执行顺序不确定）

使用实例：

```java
public static void fixedThreadPool() {
    // 创建 2 个数据级的线程池
    ExecutorService threadPool = Executors.newFixedThreadPool(2);

    // 创建任务
    Runnable runnable = new Runnable() {
        @Override
        public void run() {
            System.out.println("任务被执行,线程:" + Thread.currentThread().getName());
        }
    };

    // 线程池执行任务(一次添加 4 个任务)
    // 执行任务的方法有两种:submit 和 execute
    threadPool.submit(runnable);  // 执行方式 1:submit
    threadPool.execute(runnable); // 执行方式 2:execute
    threadPool.execute(runnable);
    threadPool.execute(runnable);
}

```





### 3.线程的分类

java中的线程分为两类，一个是**守护线程**，一个是**用户线程**。

- 守护线程是用来服务用户线程的，通过在调用start()前，设置**thread.setDaemon(true)**，可以将用户线程转化为守护线程
- java的垃圾回收线程就是一个典型的守护线程。
- 若jvm中都是守护线程，则当前jvm将退出。



### 4.Thread类相关的方法

```java
void start();

run();

String getName();

void setName();

// 返回当前线程
static Thread currentThread();

// 线程让步
//    暂停当前正在执行的线程，把执行机会让给优先级相同或更高的线程
//    若队列中没有同优先级的线程，忽略此方法
static void yield();

// 当某个程序执行调用其他线程的join方法时，调用线程将阻塞,直至被调用线程执行完毕
//    优先级较低的线程也可以获得执行
join();

// 当前线程休眠，执行其他线程，到达设定时间后，线程重新排队执行
//    抛出InterruptedException异常
static void sleep();

// 判断线程是否还活着
boolean isAlive();

// 强制结束线程，不推荐使用
stop();
```



### 5.线程的调度

- 相同优先级的线程组成先进先出队列，使用**时间片**的调度策略；
- 不同优先级的线程使用优先调度的**抢占式**策略（高优先级的线程抢占CPU）；



### 6.线程的生命周期

创建 ---> 就绪 ---> 运行 ---> 阻塞 ---> 死亡

![image-20220407133326412](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204071333072.png)

### 7.线程的同步

同步机制：在《Thinking In Java》中说，对于并发任务，我们需要某种方式来防止两个任务访问共享资源。防止这种冲突的方法就是，在某个任务访问资源时，为其加上锁，直至任务完成。 当资源被解锁时，其他任务才能访问这个资源。



#### synchronized 同步锁

首先，我们需要清楚两个概念：

> 类锁：所有对象实例共用一个锁
>
> 对象锁：一个对象一个锁，多个对象多个锁



- 任何对象都可以作为锁的对象。所有对象都具有唯一的锁（监视器）
- 当 Synchronized 修饰静态方法时，锁住的是类对象。
- 当 Synchronized 修饰实例方法时，锁住的是实例对象。
- 当 Synchronized 修饰代码块时，可以锁住指定对象。

#### ReentrantLock同步锁

ReentantLock 继承接口 Lock 并实现了接口中定义的方法，他是一种可重入锁，除了能完 成 synchronized 所能完成的所有工作外，还提供了诸如<font color=#bbbb> 可响应中断锁、可轮询锁请求、定时锁等 避免多线程死锁</font>的方法。

##### ReetrantLock实现

```java
public class MyService {
    
 	private Lock lock = new ReentrantLock();
	// Lock lock=new ReentrantLock(true);//公平锁
	private Condition condition=lock.newCondition();//创建 Condition
    
 	public void testMethod() {
 		try {
 				lock.lock();// lock 加锁
            
				// 1：通过创建 Condition 对象来使线程 wait，必须先执行 lock.lock 方法获得锁
 				condition.await();
				// 2：signal 方法唤醒
				condition.signal();
 			
 		} catch (InterruptedException e) {
 				e.printStackTrace();
 		} finally{
 				lock.unlock();
 		}
 	}
}
```

##### Condition 类和 Object 类锁方法区别区别 

1. Condition 类的 awiat 方法和 Object 类的 wait 方法等效
2. Condition 类的 signal 方法和 Object 类的 notify 方法等效 
3. Condition 类的 signalAll 方法和 Object 类的 notifyAll 方法等效 
4. ReentrantLock 类可以唤醒指定条件的线程，而 object 的唤醒是随机的



#### 比较ReentrantLock 与 synchronized

1. ReentrantLock 通过方法 lock()与 unlock()来进行加锁与解锁操作，与 synchronized 会 被 JVM 自动解锁机制不同，<font color=#bbbb>ReentrantLock 加锁后需要手动进行解锁</font>。为了避免程序出 现异常而无法正常解锁的情况，使用 ReentrantLock 必须在 finally 控制块中进行解锁操作。
2. synchronized 依赖于 JVM 而 ReenTrantLock 依赖于 API。ReenTrantLock 是 JDK 层面实现的（也就 是 API 层面，需要 lock() 和 unlock 方法配合 try/finally 语句块来完成），所以我们可以通过查看它的源代码，来看 它是如何实现的。 
3. ReenTrantLock增加了一些高级功能。主要来说主要有三点：<font color=#bbbb>①等待可中断；②可实现公平锁； ③可实现选择性通知（锁可以绑定多个条件）</font>
4. 两者都是可重入锁。“可重入锁”概念是：自己可以再次获取自己的内部锁。比如一个线程获得了某个对象的锁，此时 这个对象锁还没有释放，当其再次想要获取这个对象的锁的时候还是可以获取的，如果不可锁重入的话，就会造成死锁。



### 8.线程间的通信

#### wait() 、notify() 和notifyAll() 的区别

 wait()：令当前线程挂起并放弃CPU、同步资源并等待，使别的线程可访问并修改共享资源，而当 前线程排队等候其他线程调用notify()或notifyAll()方法唤醒，唤醒后等待重新获得对监视器的所有 权后才能继续执行。 

 notify()：唤醒正在排队等待同步资源的线程中优先级最高者结束等待 

 notifyAll ()：唤醒正在排队等待资源的所有线程结束等待. 

 **这三个方法只有在synchronized方法或synchronized代码块中才能使用**，否则会报 java.lang.IllegalMonitorStateException异常。 

 因为这三个方法必须有锁对象调用，而任意对象都可以作为synchronized的同步锁， 因此这三个方法只能在Object类中声明。



#### 小练习：银行取钱问题

1.定义一个Account类 

​		1）该Account类封装了账户编号（String）和余额（double）两个属性 

​		2）设置相应属性的getter和setter方法 

​		3）提供无参和有两个参数的构造器 

​		4）系统根据账号判断与用户是否匹配，需提供hashCode()和equals()方法的重写 

2.提供两个取钱的线程类：小明、小明’s wife 

​		1）提供了Account类的account属性和double类的取款额的属性 

​		2）提供带线程名的构造器 

​		3）run()方法中提供取钱的操作 

3.在主类中创建线程进行测试。考虑线程安全问题。

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account{
    private String accountId;
    private double balance; 
    
    @Override
    public Boolean equals(Account b){
        return this.accountId==b.accountId;
    }
}
```

```java
@Data
@AllArgsConstructor
public class Withdrawer implements Runnable{
    private Account account;
    private Double money;
    @Override
    public void Run(){
        synchronize(account){
            account.setBalance(account.getBalance()-money);
        }
    }
}

```

```java
public class test{
    public static void main(String[] args) {
		Account account = new Account("1234567", 10000);
		Withdrawer t1 = new Withdrawer( account, 8000);
		Withdrawer t2 = new Withdrawer( account, 2800);
		Thread(t1,"小明").start();
		Thread(t2,"小明的妻子").start();
	}
}
```



### 9.CyclicBarrier、CountDownLatch、Semaphore 的用法

#### CountDownLatch

CountDownLatch 类位于JUC 包下，利用它可以实现类似计数器的功能。

比如有 一个任务 A，它要等待其他 4 个任务执行完毕之后才能执行，此时就可以利用 CountDownLatch 来实现这种功能了。

```java
final CountDownLatch latch = new CountDownLatch(2);

new Thread(){public void run() {
	System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");
 	Thread.sleep(3000);
 	System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");
 	latch.countDown();
};}.start();

new Thread(){ public void run() {
	System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");
	Thread.sleep(3000);
 	System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");
 	latch.countDown();
};}.start();

System.out.println("等待 2 个子线程执行完毕...");
latch.await();
System.out.println("2 个子线程已经执行完毕");
System.out.println("继续执行主线程");
}

```



#### CyclicBarrier

字面意思回环栅栏，通过它可以实现让一组线程等待至某个状态之后再全部同时执行。

叫做回环 是因为当所有等待线程都被释放以后，CyclicBarrier 可以被重用。

我们暂且把这个状态就叫做 barrier，当调用 await()方法之后，线程就处于 barrier 了。

 **CyclicBarrier 中最重要的方法就是 await 方法，它有 2 个重载版本：** 

1. public int await()：用来挂起当前线程，直至所有线程都到达 barrier 状态再同时执行后续任 务； 
2. public int await(long timeout, TimeUnit unit)：让这些线程等待至一定的时间，如果还有 线程没有到达 barrier 状态就直接让到达 barrier 的线程执行后续任务。

```java
public static void main(String[] args) {
   int N = 4;
   CyclicBarrier barrier = new CyclicBarrier(N);
   for(int i=0;i<N;i++)
      new Writer(barrier).start();
}

static class Writer extends Thread{
      private CyclicBarrier cyclicBarrier;
      public Writer(CyclicBarrier cyclicBarrier) {
           this.cyclicBarrier = cyclicBarrier;
      }
      @Override
      public void run() {
           try {
                  Thread.sleep(5000); //以睡眠来模拟线程需要预定写入数据操作
                  System.out.println("线程"+Thread.currentThread().getName()+"写入数据完                                       毕，等待其他线程写入完毕");
 				  cyclicBarrier.await();
                } catch (InterruptedException e) {
                     e.printStackTrace();
                } catch (BrokenBarrierException e){
                     e.printStackTrace();
                }
          System.out.println("所有线程写入完毕，继续处理其他任务，比如数据操作");
      }
}
```



#### Semaphore

Semaphore 翻译成字面意思为 信号量，Semaphore 可以控制同时访问的线程个数，通过 acquire() 获取一个许可，如果没有就等待，而 release() 释放一个许可。 Semaphore 类中比较重要的几个方法： 

1. public void acquire(): 用来获取一个许可，若无许可能够获得，则会一直等待，直到获得许 可。 

2. public void acquire(int permits):获取 permits 个许可 

3. public void release() { } :释放许可。注意，在释放许可之前，必须先获获得许可。 

4. public void release(int permits) { }:释放 permits 个许可

   上面 4 个方法都会被阻塞，如果想立即得到执行结果，可以使用下面几个方法

1. public boolean tryAcquire():尝试获取一个许可，若获取成功，则立即返回 true，若获取失 败，则立即返回 false 
2. public boolean tryAcquire(long timeout, TimeUnit unit):尝试获取一个许可，若在指定的 时间内获取成功，则立即返回 true，否则则立即返回 false 
3.  public boolean tryAcquire(int permits):尝试获取 permits 个许可，若获取成功，则立即返 回 true，若获取失败，则立即返回 false 
4. public boolean tryAcquire(int permits, long timeout, TimeUnit unit): 尝试获取 permits 个许可，若在指定的时间内获取成功，则立即返回 true，否则则立即返回 false 
5. 还可以通过 availablePermits()方法得到可用的许可数目。

例子：若一个工厂有 5 台机器，但是有 8 个工人，一台机器同时只能被一个工人使用，只有使用完 了，其他工人才能继续使用。那么我们就可以通过 Semaphore 来实现：

```java
 int N = 8; //工人数
Semaphore semaphore = new Semaphore(5); //机器数目
for(int i=0;i<N;i++)
new Worker(i,semaphore).start();
}
static class Worker extends Thread{
private int num;
private Semaphore semaphore;
public Worker(int num,Semaphore semaphore){
this.num = num;
this.semaphore = semaphore;
}
@Override
public void run() {
try {
semaphore.acquire();
System.out.println("工人"+this.num+"占用一个机器在生产...");
Thread.sleep(2000);
System.out.println("工人"+this.num+"释放出机器");
semaphore.release();
} catch (InterruptedException e) {
e.printStackTrace();
}
}
```

 CountDownLatch 和 CyclicBarrier 都能够实现线程之间的等待，只不过它们侧重点不 同；

CountDownLatch 一般用于某个线程 A 等待若干个其他线程执行完任务之后，它才执行；而 CyclicBarrier 一般用于一组线程互相等待至某个状态，然后这一组线程再同时 执行；

另外，CountDownLatch 是不能够重用的，而 CyclicBarrier 是可以重用的。  Semaphore 其实和锁有点类似，它一般用于控制对某组资源的访问权限。



### 10.如何解决CAS的ABA问题

CAS（compare and swap）的原理是拿期望的值A和原本的内存值V作比较，如果相同则更新成新的值B。

#### 解决方案

JDK的atomic包里提供了一个类**AtomicStampedReference**来解决ABA问题。其实就是版本号机制。

如果当前引用 == 预期引用，并且当前标志等于预期标志，则以原子方式将该引用和该标志的值设置为给定的更新值。

源码如下：

```java
/**
 *expectedReference - 该引用的预期值
 *newReference - 该引用的新值
 *expectedStamp - 该标志的预期值
 *newStamp - 该标志的新值
 */
public boolean compareAndSet(V   expectedReference,
                                 V   newReference,
                                 int expectedStamp,
                                 int newStamp) {
        Pair<V> current = pair;
        return
            expectedReference == current.reference &&
            expectedStamp == current.stamp &&
            ((newReference == current.reference &&
              newStamp == current.stamp) ||
             casPair(current, Pair.of(newReference, newStamp)));
    }
```

#### 最佳实践

```java
    private static AtomicStampedReference<Integer> atomicStampedRef =
            new AtomicStampedReference<Integer>(100, 0);

        Thread refT1 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    TimeUnit.SECONDS.sleep(1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                atomicStampedRef.compareAndSet(100, 101,
                        atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1);
                log("thread refT1:" + atomicStampedRef.getReference());
                atomicStampedRef.compareAndSet(101, 100,
                        atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1);
                log("thread refT1:" + atomicStampedRef.getReference());
            }
        });

        Thread refT2 = new Thread(new Runnable() {
            @Override
            public void run() {
                int stamp = atomicStampedRef.getStamp();
                log("before sleep : stamp = " + stamp);    // stamp = 0
                try {
                    TimeUnit.SECONDS.sleep(2);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                log("after sleep : stamp = " + atomicStampedRef.getStamp());//stamp = 1
                boolean c3 = atomicStampedRef.compareAndSet(100, 101, stamp, stamp + 1);
                log("thread refT2:" + atomicStampedRef.getReference() + ",c3 is " + c3);        //true
            }
        });

        refT1.start();
        refT2.start();
    }

    private static void log(String logString) {
        System.out.println(logString);
    }
```



### 10.指令重排序：

**简单来说，就是指你在程序中写的代码，在执行时并不一定按照写的顺序。**

在Java中，JVM能够根据处理器特性（CPU多级缓存系统、多核处理器等）适当对机器指令进行重排序，最大限度发挥机器性能。

参考链接： https://zhuanlan.zhihu.com/p/138819184



### 11.session和cookie的区别

cookie是客户端的，session是服务端的。

cookie存储于客户端，记录web服务器的信息，每次上网时都会先查看对应的cookie信息，比如购物时，使用cookie记录购物车信息。 

session是记录客户机的信息，SessionID是session的唯一标识，使用session可以记录客户端的请求等。





## 四、IO流





## 五、JVM

主要分为六大块：

**①Java内存区域、②JVM内存管理、③虚拟机垃圾收集器、④虚拟机垃圾算法、⑤JVM调优、⑥Java类加载机制**



### 线程

这里所说的线程指程序执行过程中的一个线程实体。

JVM 允许一个应用并发执行多个线程。 Hotspot JVM 中的 Java 线程与原生操作系统线程有直接的映射关系。

<font color=#bbbb>当线程本地存储、缓 冲区分配、同步对象、栈、程序计数器等准备好以后，就会创建一个操作系统原生线程。</font>

Java 线程结束，原生线程随之被回收。操作系统负责调度所有线程，并把它们分配到任何可用的 CPU 上。当原生线程初始化完毕，就会调用 Java 线程的 run() 方法。当线程结束时, 会释放原生线程和 Java 线程的所有资源。

Hotspot JVM 后台运行的系统线程主要有下面几个： 

| 虚拟机线程 （VM thread） | 这个线程等待 JVM 到达安全点操作出现。这些操作必须要在独立的线程里执行，因为当 堆修改无法进行时，线程都需要 JVM 位于安全点。这些操作的类型有：stop-theworld 垃圾回收、线程栈 dump、线程暂停、线程偏向锁（biased locking）解除。 |
| ------------------------ | ------------------------------------------------------------ |
| **周期性任务线程**| 这线程负责定时器事件（也就是中断），用来调度周期性操作的执行。 |
| **GC 线程**| 这些线程支持 JVM 中不同的垃圾回收活动。                      |
| **编译器线程**| 这些线程在运行时将字节码动态编译成本地平台相关的机器码。     |
| **信号分发线程** | 这个线程接收发送到 JVM 的信号并调用适当的 JVM 方法处理。     |

###  内存区域

JVM 内存区域主要分为

- 线程私有区域：`程序计数器`、`虚拟机栈`、`本地方法栈`

- 线程共享区域：`JAVA 堆`、`方法区`

- 直接内存：`不受JVM GC管理`

**线程私有数据区域** 生命周期与线程相同, <font color=#bbbb>依赖用户线程的启动/结束，而创建/销毁(在 Hotspot VM 内</font>, 每个线程都与操作系统的本地线程直接映射, 因此这部分内存区域的存/否跟随本地线程的 生/死对应)。

**线程共享区域** <font color=#bbbb>随虚拟机的启动/关闭而创建/销毁。</font>

**直接内存** <font color=#bbbb>并不是 JVM 运行时数据区的一部分</font>, 但也会被频繁的使用: 例如 NIO 提 供了基于 Channel 与 Buffer 的 IO 方式, 它可以<font color=#bbbb>使用 Native 函数库直接分配堆外内存</font>, 然后使用 DirectByteBuffer 对象作为这块内存的引用进行操作, 这样就避免了在 Java 堆和 Native 堆中来回复制数据, 因此在一些场景中可以显著提高性能。

![image-20220418225937866](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204182259266.png)

#### 程序计数器(线程私有)

一块较小的内存空间, <font color=#bbbb>是当前线程所执行的字节码的行号指示器</font>，每条线程都要有一个独立的程序计数器，这类内存也称为“线程私有”的内存。 

正在执行 java 方法的话，计数器记录的是虚拟机字节码指令的地址（当前指令的地址）。如果还是 Native 方法，则为空。 这个内存区域是唯一一个在虚拟机中没有规定任何 OutOfMemoryError 情况的区域。

#### 虚拟机栈(线程私有) 

是描述java方法执行的内存模型，每个方法在执行的同时都会创建一个栈帧（Stack Frame） 用于存储局部变量表、操作数栈、动态链接、方法出口等信息。每一个方法从调用直至执行完成 的过程，就对应着一个栈帧在虚拟机栈中入栈到出栈的过程。

<img src="https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204192159839.png" alt="image-20220419215913693" style="zoom:75%;" />

#### 本地方法栈(线程私有) 

> Native本地方法：
>
> 1.JVM的实现，为了与操作系统底层进行交互，就使用了本地方法。
> 2.JVM自己的代码，有一部分使用C实现的，这些代码的使用也需要使用本地方法。

本地方法区和 Java Stack 作用类似, 区别是虚拟机栈为执行 Java 方法服务, 而本地方法栈则为 Native 方法服务, 如果一个 VM 实现使用 C-linkage 模型来支持 Native 调用, 那么该栈将会是一个 C 栈，但 HotSpot VM 直接就把本地方法栈和虚拟机栈合二为一。

#### 堆（Heap-线程共享）

**又称运行时数据区。**是被线程共享的一块内存区域，创建的对象和数组都保存在 Java 堆内存中，也是垃圾收集器进行 垃圾收集的最重要的内存区域。由于现代 VM 采用分代收集算法, 因此 Java 堆从 GC 的角度还可以 细分为: <font color=#bbbb>新生代【Eden 区、From Survivor 区、 To Survivor 区】和老年代。</font>

#### 方法区/永久代（线程共享） 

即我们常说的永久代(Permanent Generation), 用于存储被 JVM 加载的类信息、常量、静 态变量、即时编译器编译后的代码等数据. 

<font color=#bbbb>HotSpot VM把GC分代收集扩展至方法区, 即使用Java 堆的永久代来实现方法区</font>, 这样 HotSpot 的垃圾收集器就可以像管理 Java 堆一样管理这部分内存, 而不必为方法区开发专门的内存管理器(永久代的内存回收的主要目标是针对常量池的回收和类型 的卸载, 因此收益一般很小)。 

运行时常量池（Runtime Constant Pool）是方法区的一部分。Class 文件中除了有类的版 本、字段、方法、接口等描述等信息外，还有一项信息是常量池 ，用于存放编译期生成的各种字面量和符号引用，这部分内容将在类加 载后存放到方法区的运行时常量池中。

 Java 虚拟机对 Class 文件的每一部分（自然也包括常量 池）的格式都有严格的规定，每一个字节用于存储哪种数据都必须符合规范上的要求，这样才会 被虚拟机认可、装载和执行。



### 运行时内存

Java 堆从 GC 的角度还可以细分为: 新生代【Eden 区、From Survivor 区、 To Survivor 区】和老年 代。

![image-20220419235356742](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204192353112.png)

#### 新生代

是用来存放新生的对象。一般占据堆的 1/3 空间。由于频繁创建对象，所以新生代会频繁触发 MinorGC 进行垃圾回收。

 **\- 伊甸园（Eden）：**这是对象最初诞生的区域，并且对大多数对象来说，这里是它们唯一存在过的区域。 

 **\- 幸存者乐园（SurvivorFrom）：**伊甸园幸存对象会被挪到这里。 上一次 GC 的幸存者，作为这一次 GC 的被扫描者。

 **\- 幸存者乐园（SurvivorTo）：**保留了一次 MinorGC 过程中的幸存者。

----



#### **MinorGC 的过程（复制->清空->互换）**

 MinorGC 采用复制算法。

**1：Eden、SurvivorFrom 复制到 SurvivorTo，年龄+1** 

首先，把 Eden 和 SurvivorFrom 区域中存活的对象复制到 SurvivorTo 区域（如果有对象的年 龄以及达到了老年的标准，则赋值到老年代区），同时把这些对象的年龄+1（如果 SurvivorTo 不 够位置了就放到老年区）；

**2：清空 Eden、SurvivorFrom** 

然后，清空 Eden 和 SurvivorFrom 中的对象； 

**3：SurvivorTo 和 SurvivorFrom互换** 

最后，SurvivorTo 和 SurvivorFrom互换，原 SurvivorTo 成为下一次 GC 时的 SurvivorFrom区。

>  从年轻代空间（包括 Eden 和 Survivor 区域）回收内存被称为 Minor GC。 Major GC 是清理永久代。Full GC 是清理整个堆空间—包括年轻代和永久代。

----



#### 老年代

主要存放应用程序中生命周期长的内存对象。 

老年代的对象比较稳定，所以 MajorGC 不会频繁执行。在进行 MajorGC 前一般都先进行 了一次 MinorGC，使得有新生代的对象晋身入老年代，导致空间不够用时才触发。当无法找到足 够大的连续空间分配给新创建的较大对象时也会提前触发一次 MajorGC 进行垃圾回收腾出空间。 

MajorGC 采用 <font color=#bbbb>标记清除算法：</font>首先扫描一次所有老年代，标记出存活的对象，然后回收没 有标记的对象。MajorGC 的耗时比较长，因为要扫描再回收。MajorGC 会产生内存碎片，为了减 少内存损耗，我们一般需要进行合并或者标记出来方便下次直接分配。当老年代也满了装不下的 时候，就会抛出 OOM（Out of Memory）异常。



### 垃圾回收与算法

主要理清以下几点：GC要做的三件事、如何确定垃圾、垃圾收集算法、垃圾收集器、参数。

#### 如何确定垃圾 or 如何判断对象是否死亡

- **引用计数法**

  在 Java 中，引用和对象是有关联的。如果要操作对象则必须用引用进行。因此，很显然一个简单 的办法是通过引用计数来判断一个对象是否可以回收。简单说，即一个对象如果没有任何与之关 联的引用，即他们的引用计数都不为 0，则说明对象不太可能再被用到，那么这个对象就是可回收 对象.

- **可达性分析** 

  为了解决引用计数法的循环引用问题，Java 使用了可达性分析的方法。通过一系列的“GC roots” 对象作为起点搜索。如果在“GC roots”和一个对象之间没有可达路径，则称该对象是不可达的。 

   要注意的是，不可达对象不等价于可回收对象，不可达对象变为可回收对象至少要经过两次标记 过程。两次标记后仍然是可回收对象，则将面临回收。

---

#### 垃圾收集算法

##### 标记清除算法（Mark-Sweep） 

最基础的垃圾回收算法，分为两个阶段，标注和清除。

<font color=#bbbb>标记阶段</font>标记出所有需要回收的对象，<font color=#bbbb>清除阶段</font>回收被标记的对象所占用的空间。如图 

![image-20220425231546970](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204252315734.png)

从图中我们就可以发现，该算法最大的问题是<font color=#bbbb>内存碎片化严重</font>，后续可能发生大对象不能找到可利用空间的问题。

---

##### 复制算法（copying） 

为了解决 Mark-Sweep 算法内存碎片化的缺陷而被提出的算法。按内存容量将内存划分为等大小 的两块。每次只使用其中一块，当这一块内存满后将尚存活的对象复制到另一块上去，把已使用 的内存清掉，如图：

![image-20220425232619309](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204252326499.png)

这种算法虽然实现简单，内存效率高，不易产生碎片，但是最大的问题是可用内存被压缩到了原 本的一半。且存活对象增多的话，Copying 算法的效率会大大降低。

---

##### 标记整理算法(Mark-Compact) 

结合了以上两个算法，为了避免缺陷而提出。标记阶段和 Mark-Sweep 算法相同，标记后不是清理对象，而是将存活对象移向内存的一端。然后清除端边界外的对象。如图：

![image-20220425234615442](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204252346612.png)

---

##### 分代收集算法

分代收集法是目前大部分 JVM 所采用的方法，其核心思想是根据对象存活的不同生命周期将内存 划分为不同的域，一般情况下将 GC 堆划分为老生代(Tenured/Old Generation)和新生代(Young Generation)。老生代的特点是每次垃圾回收时只有少量对象需要被回收，新生代的特点是每次垃 圾回收时都有大量垃圾需要被回收，因此可以根据不同区域选择不同的算法。

###### 新生代与复制算法 

每次垃圾收集都能发现大批对象已死, 只有少量存活. 因此选用复制算法, 只需要付出少量 存活对象的复制成本就可以完成收集.

但通常并不是按照 1：1 来划分新生代。一般将新生代 划分为一块较大的 Eden 空间和两个较小的 Survivor 空间(From Space, To Space)，每次使用 Eden 空间和其中的一块 Survivor 空间，当进行回收时，将该两块空间中还存活的对象复制到另 一块 Survivor 空间中。

![image-20220425234855761](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204252348919.png)

###### 老年代与标记复制算法

因为对象存活率高、没有额外空间对它进行分配担保, 就必须采用“标记—清理”或“标 记—整理”算法来进行回收, 不必进行内存复制, 且直接腾出空闲内存.

1. JAVA 虚拟机提到过的处于方法区的永生代(Permanet Generation)，它用来存储 class 类， 常量，方法描述等。对永生代的回收主要包括废弃常量和无用的类。 
2. 对象的内存分配主要在新生代的 Eden Space 和 Survivor Space 的 From Space(Survivor 目 前存放对象的那一块)，少数情况会直接分配到老生代。 
3. 当新生代的 Eden Space 和 From Space 空间不足时就会发生一次 GC，进行 GC 后，Eden Space 和 From Space 区的存活对象会被挪到 To Space，然后将 Eden Space 和 From Space 进行清理。
4. 如果 To Space 无法足够存储某个对象，则将这个对象存储到老生代。 
5. 在进行 GC 后，使用的便是 Eden Space 和 To Space 了，如此反复循环。 
6. 当对象在 Survivor 区躲过一次 GC 后，其年龄就会+1。<font color=#bbbb>默认情况下年龄到达 15 的对象会被 移到老生代中。</font>

---

##### 分区收集算法

分区算法则将整个堆空间划分为连续的不同小区间, 每个小区间独立使用, 独立回收. 这样做的 好处是可以控制一次回收多少个小区间 , 根据目标停顿时间, 每次合理地回收若干个小区间(而不是 整个堆), 从而减少一次 GC 所产生的停顿。

---

#### 常见的垃圾回收器有那些？ 

##### Serial 垃圾收集器

（单线程、复制算法） 

Serial 是最基本垃圾收集器，使用复制算法，曾经是JDK1.3.1 之前新生代唯一的垃圾 收集器。Serial 是一个单线程的收集器，它不但只会使用一个 CPU 或一条线程去完成垃圾收集工 作，并且在进行垃圾收集的同时，必须暂停其他所有的工作线程，直到垃圾收集结束。 Serial 垃圾收集器虽然在收集垃圾过程中需要暂停所有其他的工作线程，但是它简单高效，对于限 定单个 CPU 环境来说，没有线程交互的开销，可以获得最高的单线程垃圾收集效率，因此 Serial 垃圾收集器依然是 java 虚拟机运行在 Client 模式下默认的新生代垃圾收集器。

##### ParNew 垃圾收集器

（Serial+多线程） 

ParNew 垃圾收集器其实是 Serial 收集器的多线程版本，也使用复制算法，除了使用多线程进行垃圾收集之外，其余的行为和 Serial 收集器完全一样，ParNew 垃圾收集器在垃圾收集过程中同样也要暂停所有其他的工作线程。

ParNew 收集器默认开启和 CPU 数目相同的线程数，可以通过 -XX : ParallelGCThreads 参数来限 制垃圾收集器的线程数。【Parallel：平行的】 ParNew 虽然是除了多线程外和Serial 收集器几乎完全一样，但是 ParNew 垃圾收集器是很多 java 虚拟机运行在 Server 模式下新生代的默认垃圾收集器。



##### Parallel Scavenge 收集器

（多线程复制算法、高效） 

Parallel Scavenge 收集器也是一个新生代垃圾收集器，同样使用复制算法，也是一个多线程的垃圾收集器，它重点关注的是程序达到一个可控制的吞吐量（Thoughput，CPU 用于运行用户代码 的时间/CPU 总消耗时间，即吞吐量=运行用户代码时间/(运行用户代码时间+垃圾收集时间)）， 高吞吐量可以最高效率地利用 CPU 时间，尽快地完成程序的运算任务，主要适用于在后台运算而 不需要太多交互的任务。自适应调节策略也是 ParallelScavenge 收集器与 ParNew 收集器的一个 重要区别。



##### Serial Old 收集器

（单线程标记整理算法 ） 

Serial Old 是 Serial 垃圾收集器年老代版本，它同样是个单线程的收集器，使用标记-整理算法， 这个收集器也主要是运行在 Client 默认的 java 虚拟机默认的年老代垃圾收集器。 在 Server 模式下，主要有两个用途： 

1. 在 JDK1.5 之前版本中与新生代的 Parallel Scavenge 收集器搭配使用。 
2. 作为年老代中使用 CMS 收集器的后备垃圾收集方案。



##### Parallel Old 收集器

（多线程标记整理算法） 

Parallel Old 收集器是Parallel Scavenge的年老代版本，使用多线程的标记-整理算法，在 JDK1.6 才开始提供。 在 JDK1.6 之前，新生代使用 Parallel Scavenge 收集器只能搭配年老代的 Serial Old 收集器，只 能保证新生代的吞吐量优先，无法保证整体的吞吐量，Parallel Old 正是为了在年老代同样提供吞 吐量优先的垃圾收集器，如果系统对吞吐量要求比较高，可以优先考虑新生代 Parallel Scavenge 和年老代 Parallel Old 收集器的搭配策略。



---





强引用、软引用、弱引用、虚引用



如何判断一个常量是废弃常量 

如何判断一个类是无用的类 

#### 

介绍一下CMS,G1收集器。 

Minor GC 和 Full GC 有什么不同呢？





###  Java 对象的创建过程

五步，建议能默写出来并且要知道每一步虚拟机做了什么

![image-20220424211620812](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204242116345.png)

![image-20220424211820839](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202204242118004.png)

### 对象的访问定位的两种方式（句柄和直接指针两种方式） 

### 拓展问题: String类和常量池 

### 8种基本类型的包装类和常量池 

 HotSpot为什么要分为新生代和老年代？ 



### java类加载机制









## 二、Spring

### １.Bean的生命周期

创建、

IOC注入、

getBeanName、

BeanNameFactory、

ApplicationContextAware、

PostConstructBeforeInitiation、

init、

PostConstructAfterInitiation、

destroy



### ２.SpringMVC的工作原理？

- 用户向服务器发送请求，通过server.xml文件，请求被前端控制器DispatchServlet捕获；
- DispatchServlet对URL进行解析，得到请求资源标识符（URI），通过HandlerMapping找到合适的处理器HandlerExcutionChain;
- 根据得到的处理器，DispatchServlet选择合适的适配器handlerAdapter处理请求；
- handler处理完请求后，返回一个ModelAndView对象给DispatchServlet；
- DispatchServlet将此对象通过ViewResolver进行处理，并得到渲染视图；
- 最后将Model中的参数进行解析，最终呈现出完整的视图返回给客户端；

### ３.常用注解有哪些？

### ４.谈谈你对Spring的理解

Spring是一个开源框架，为简化企业级应用开发而生，Spring是一个IOC和AOP容器框架

### ５.Spring容器的主要核心是：



![Spring的设计模式](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202202050318374.png)



## 三、SQL

### mysql和oracle的区别

### innoDB和MyIsam的区别

### 慢查询的原因

### 行级锁表级锁

### 1.sql注入是什么？#{}和${}的区别是什么?

sql注入是指通过web表单输入恶意sql语句，激发数据库漏洞，而不是按设计者意图去执行sql语句。举例：select * from def_user where username=" <u>admin "  or  "a"="a</u> "恒成立；

#{}是通过预编译处理，如select * from user where username=?,sql语义不会发生改变，在很大程度上可以防止sql注入

${}是字符串替换。在处理时，将 它替换成变量的值，不安全。

### 2.MySQL性能优化有哪些？

- 使用limit1
- 选择正确的数据库引擎
- 用not exists代替not in
- 对操作符进行优化，尽量不采用索引的操作符





## 四、Mybatis

### 1、什么是 Mybatis？

（1） Mybatis 是一个半 ORM（对象关系映射）框架，它内部封装了 JDBC，开
发时只需要关注 SQL 语句本身，不需要花费精力去处理加载驱动、创建连接、
创建 statement 等繁杂的过程。程序员直接编写原生态 sql，可以严格控制
sql 执行性能，灵活度高。
（2） MyBatis 可以使用 XML 或注解来配置和映射原生信息，将 POJO 映射成
数据库中的记录，避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果
集。
（3） 通过 xml 文件或注解的方式将要执行的各种 statement 配置起来，并通
过 java 对象和 statement 中 sql 的动态参数进行映射生成最终执行的 sql
语句，最后由 mybatis 框架执行 sql 并将结果映射为 java 对象并返回。
（从执行 sql 到返回 result 的过程）。



## 五、Redis

![](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/202202050319649.png)

## 六、RabbitMQ

### 1、什么是rabbitmq？

**答：**

采用AMQP高级消息队列协议的一种消息队列技术,最大的特点就是消费并不需要确保提供方存在,实现了服务之间的高度解耦。

### 2、为什么要使用rabbitmq？

**答：** 1、在分布式系统下具备异步,削峰,负载均衡等一系列高级功能；

2、拥有持久化的机制，进程消息，队列中的信息也可以保存下来。

3、实现消费者和生产者之间的解耦。

4、对于高并发场景下，利用消息队列可以使得同步访问变为串行访问达到一定量的限流，利于数据库的操作。

5、可以使用消息队列达到异步下单的效果，排队中，后台进行逻辑下单。

### 4、如何确保消息正确地发送至RabbitMQ？如何确保消息接收方消费了消息？

答：
发送方确认模式
1.将信道设置成confirm模式（发送方确认模式），则所有在信道上发布的消息都会被指派一个唯一的ID。
2.一旦消息被投递到目的队列后，或者消息被写入磁盘后（可持久化的消息），信道会发送一个确认给生产者（包含消息唯一 ID）。
3.如果 RabbitMQ发生内部错误从而导致消息丢失，会发送一条nack（notacknowledged，未确认）消息。发送方确认模式是异步的，生产者应用程序在等待确认的同时，可以继续发送消息。当确认消息到达生产者应用程序，生产者应用程序的回调方法就会被触发来处理确认消息。
接收方确认机制
接收方消息确认机制
消费者接收每一条消息后都必须进行确认（消息接收和消息确认是两个不同操作）。只有消费者确认了消息，RabbitMQ才能安全地把消息从队列中删除。这里并没有用到超时机制，RabbitMQ仅通过Consumer的连接中断来确认是否需要重新发送消息。也就是说，只要连接不中断，RabbitMQ给了Consumer足够长的时间来处理消息。保证数据的最终一致性；



### 5.如何避免消息重复投递或重复消费？

**答：**

在消息生产时，MQ内部针对每条生产者发送的消息生成一个inner-msg-id，作为去重的依据（消息投递失败并重传），避免重复的消息进入队列；

在消息消费时，要求消息体中必须要有一个 bizId（对于同一业务全局唯一，如支付ID、订单ID、帖子ID 等）作为去重的依据，避免同一条消息被重复消费。



### 6.死信队列

一个消息是有死亡状态的，它会被发送到一个指定的队列中，这个队列是一个普通的队列，根据他的功能，我们叫他死信队列。



### 8、消息怎么路由？

答：
消息提供方->路由->一至多个队列
消息发布到交换器时，消息将拥有一个路由键（routing key），在消息创建时设定。
通过队列路由键，可以把队列绑定到交换器上。
消息到达交换器后，RabbitMQ 会将消息的路由键与队列的路由键进行匹配（针对不同的交换器有不同的路由规则）；
常用的交换器主要分为一下三种
1.fanout：如果交换器收到消息，将会广播到所有绑定的队列上
2.direct：如果路由键完全匹配，消息就被投递到相应的队列
3.topic：可以使来自不同源头的消息能够到达同一个队列。 使用topic交换器时，可以使用通配符



### 七、ehcache

ehcache直接在jvm虚拟机中缓存，速度快，效率高；但是缓存共享麻烦，集群分布式应用不方便。

Spring Cache 是 Spring 提供的一整套的缓存解决方案。虽然它本身并没有提供缓存的实现，但是它提供了一整套的接口和代码规范、配置、注解等，这样它就可以整合各种缓存方案了，比如 Redis、Ehcache，我们也就不用关心操作缓存的细节。

Spring 提供了四个注解来声明缓存规则。@Cacheable，@CachePut，@CacheEvict，@Caching。



### 八、简历说明

独立的模块设计+使用count判断是否存在，改为limit 1