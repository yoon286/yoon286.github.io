---
title: Java语言特性
date: 2025-07-12 23:27:31
tags: 
- Java
categories: 
- 学习
- Java
- 语言特性
---



file:///D:/Download/%E4%B8%8B%E8%BD%BD/%E9%9D%A2%E8%AF%95%E7%AA%81%E5%87%BB-Java%E5%9F%BA%E7%A1%80%EF%BC%88%E6%9A%97%E8%89%B2%EF%BC%89.pdf

https://javaguide.cn/java/io/io-model.html#nio-non-blocking-new-i-o



集合部分：

file:///D:/Download/%E6%96%87%E6%A1%A3/WeChat%20Files/wxid_y5fy507qqs9q22/FileStorage/File/2025-07/%E9%9D%A2%E8%AF%95%E7%AA%81%E5%87%BB-Java%E9%9B%86%E5%90%88%EF%BC%88%E4%BA%AE%E8%89%B2%EF%BC%89.pdf



### 一、集合



Java 集合，也叫作容器，主要是由两⼤接⼝派⽣⽽来：⼀个是 `Collection` 接⼝，主要⽤于存放单⼀ 元素；另⼀个是 `Map` 接口，主要⽤于存放键值对。对于 `Collection` 接⼝，下⾯⼜有三个主要的子接⼝： `List` 、 `Set` 、 `Queue` 。 Java 集合框架如下图所示：

![image-20250714190257198](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/image-20250714190257198.png)

#### List

##### ArrayList 和 Array（数组）的区别？

##### ArrayList 与 LinkedList 区别?

##### 说⼀说 ArrayList 的扩容机制吧

##### 集合中的 fail-fast 和 fail-safe 是什么



#### Set



##### Comparable 和 Comparator 的区别

Comparable来自于java.lang包，排序方法是compareTo(Object b)

Comparator来自于java.utils包，排序方法是comparator(Object a, Object b)



##### ⽐较 HashSet、LinkedHashSet 和 TreeSet 三者的异同

#### Queue



#### Map



### 二、多线程





### 三、输入输出流



### 四、高并发



### 五、设计模式

设计模式（Design pattern）是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性。设计模式的三个分类：

**创建型模式：**对象实例化的模式，创建型模式用于解耦对象的实例化过程。

**结构型模式：**把类或对象结合在一起形成一个更大的结构。

**行为型模式：**类和对象如何交互，及划分责任和算法。

参考视频：https://www.bilibili.com/video/BV1vNN4zaEo7?spm_id_from=333.788.videopod.episodes&vd_source=5c14f766fdfaa0f3c9f5b3c4857d0bd2&p=8

![img](https://cdn.jsdelivr.net/gh/yoon286/Pic@main/img/401339-20170928225241215-295252070.png)

| 模式       | 核心用途     | 典型场景               |
| :--------- | :----------- | :--------------------- |
| 单例模式   | 全局唯一实例 | 配置管理、连接池       |
| 工厂模式   | 解耦对象创建 | 支付系统、日志记录器   |
|            |              |                        |
| 观察者模式 | 状态变更通知 | 事件系统、消息订阅     |
| 策略模式   | 灵活切换算法 | 排序、支付策略         |
|            |              |                        |
| 适配器模式 | 兼容旧接口   | 系统集成、第三方库适配 |
| 装饰器模式 | 动态扩展功能 | I/O流、UI组件增强      |

#### 1. 单例模式（Singleton）

**目的**：确保一个类只有一个实例。
**示例**：数据库连接池

```java
public class DatabaseConnection {
    private static DatabaseConnection instance;
    
    private DatabaseConnection() {}  // 私有构造器
    
    public static synchronized DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }
}
// 使用
DatabaseConnection db = DatabaseConnection.getInstance();
```

------

#### 2. 工厂模式（Factory）

**目的**：将对象创建逻辑封装起来。实际是利用了面向对象的多态，创建同一父类的不同子类对象。
**示例**：支付方式工厂

```java
public interface Payment {
    void pay(int amount);
}

class CreditCard implements Payment {
    @Override
    public void pay(int amount) {
        System.out.println("信用卡支付：" + amount);
    }
}

class PayPal implements Payment {
    @Override
    public void pay(int amount) {
        System.out.println("PayPal支付：" + amount);
    }
}

public class PaymentFactory {
    public Payment createPayment(String type) {
        return switch (type.toLowerCase()) {
            case "creditcard" -> new CreditCard();
            case "paypal" -> new PayPal();
            default -> throw new IllegalArgumentException("未知支付类型");
        };
    }
}
// 使用
PaymentFactory factory = new PaymentFactory();
Payment payment = factory.createPayment("PayPal");
payment.pay(100);
```

------

#### 3. 观察者模式（Observer）

**目的**：对象状态变化时自动通知依赖对象。
**示例**：新闻订阅系统

```
import java.util.*;

interface Subscriber {
    void update(String news);
}

class NewsAgency {
    private List<Subscriber> subscribers = new ArrayList<>();
    
    public void subscribe(Subscriber s) {
        subscribers.add(s);
    }
    
    public void publishNews(String news) {
        for (Subscriber s : subscribers) {
            s.update(news);
        }
    }
}

class User implements Subscriber {
    private String name;
    public User(String name) { this.name = name; }
    
    @Override
    public void update(String news) {
        System.out.println(name + " 收到新闻: " + news);
    }
}
// 使用
NewsAgency agency = new NewsAgency();
agency.subscribe(new User("张三"));
agency.subscribe(new User("李四"));
agency.publishNews("Java 21 发布！");
```

------

#### 4. 装饰器模式（Decorator）

**目的**：动态扩展对象功能。
**示例**：咖啡加料系统

```
interface Coffee {
    double getCost();
    String getDescription();
}

class SimpleCoffee implements Coffee {
    @Override public double getCost() { return 2.0; }
    @Override public String getDescription() { return "基础咖啡"; }
}

abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;
    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }
}

class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) { super(coffee); }
    @Override public double getCost() { return decoratedCoffee.getCost() + 0.5; }
    @Override public String getDescription() { 
        return decoratedCoffee.getDescription() + ", 加牛奶"; 
    }
}
// 使用
Coffee coffee = new SimpleCoffee();
coffee = new MilkDecorator(coffee);  // 动态添加功能
System.out.println(coffee.getDescription() + " 价格: $" + coffee.getCost());
```

------

#### 5. 策略模式（Strategy）

**目的**：封装可互换的算法。可以看成是包装后的工厂模式，将对象的创建放在上下文中，隐藏了工厂模式中通过Factory创建对象的申明，使用成本更小。
**示例**：排序算法切换

```java
interface SortStrategy {
    void sort(int[] array);
}

class BubbleSort implements SortStrategy {
    @Override
    public void sort(int[] array) {
        System.out.println("使用冒泡排序");
        // 实现略
    }
}

class QuickSort implements SortStrategy {
    @Override
    public void sort(int[] array) {
        System.out.println("使用快速排序");
        // 实现略
    }
}

class Sorter {
    private SortStrategy strategy;
    public void setStrategy(SortStrategy strategy) {
        this.strategy = strategy;
    }
    public void executeSort(int[] array) {
        strategy.sort(array);
    }
}
// 使用
int[] data = {5, 2, 9, 1};
Sorter sorter = new Sorter();
sorter.setStrategy(new QuickSort());  // 动态切换算法
sorter.executeSort(data);
```

------

#### 6. 适配器模式（Adapter）

**目的**：使不兼容接口协同工作。
**示例**：旧式播放器适配新接口

```
interface MediaPlayer {
    void play(String fileType, String fileName);
}

class LegacyPlayer {
    public void playLegacy(String fileName) {
        System.out.println("播放旧格式文件: " + fileName);
    }
}

class PlayerAdapter implements MediaPlayer {
    private LegacyPlayer legacyPlayer = new LegacyPlayer();
    
    @Override
    public void play(String fileType, String fileName) {
        if (fileType.equals("legacy")) {
            legacyPlayer.playLegacy(fileName);  // 适配旧接口
        } else {
            System.out.println("不支持格式: " + fileType);
        }
    }
}
// 使用
MediaPlayer player = new PlayerAdapter();
player.play("legacy", "old_song.dat");
```

### 

