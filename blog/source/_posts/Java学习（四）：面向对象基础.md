---
title:  Java学习（四）：面向对象基础
date: 2020-02-19 21:48:24
tags:
	- Java
---
# 4.1 面向过程和面向对象
- **面向过程和面向对象**都是对软件分析、设计和开发的一种思想，它指导着人们以不同的方式去分析、设计和开发软件。
1. 都是解决问题的思维方式，都是代码组织的方式。
2. 解决简单问题可以使用面向过程
3. 解决复杂问题：宏观上使用面向对象把握，微观处理上仍然是面向过程。
<!--more-->
# 4.2 对象的进化史
- 数据管理和企业管理共通之处
![对象的进化史](https://img-blog.csdnimg.cn/20200219155743369.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
1. 对象说白了也是一种数据结构(对数据的管理模式)，将数据和数据的行为放到了一起。
2. 在内存上，对象就是一个内存块，存放了相关的数据集合!
3. 对象的本质就一种数据的组织方式!

# 4.3 对象和类的概念
- 对象是具体的事物;类是对对象的抽象;

- 类可以看成一类对象的模板，对象可以看成该类的一个具体实例。

- 类是用于描述同一类型的对象的一个抽象概念，类中定义了这一类对象所应具有的共同的属性、方法。

## 4.3.1 第一个类的定义

```java
public class SxtStu {
    //属性（成员变量）
    int id;
    String sname;
    int age;  
    //方法
    void study(){
        System.out.println("我正在学习！");
    }  
    //构造方法
   SxtStu(){
   }
}
```

## 4.3.2 属性
  - 属性用于定义该类或该类对象包含的数据或者说静态特征。
- 属性作用范围是整个类体。

- 在定义成员变量时可以对其初始化，如果不对其初始化，Java使用默认的值对其初始化。
![成员变量的默认值](https://img-blog.csdnimg.cn/20200219164213307.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 4.3.3 方法
- 方法用于定义该类或该类实例的行为特征和功能实现。
- 方法是类和对象行为特征的抽象。
- 方法很类似于面向过程中的函数。
- 面向过程中，函数是最基本单位，整个程序由一个个函数调用组成。
- 面向对象中，整个程序的基本单位是类，方法是从属于类和对象的。
## 4.3.4 一个典型类的定义

```java
public class Stu {
	int age;
	String name;
	int id;
	Computer comp;
	
	void study() {
		System.out.println(name+" is studying with "+comp.brand+" computer.");
	}
	
	void play() {
		System.out.println("Playing...");
	}
	public static void main(String[] arg) {
		Stu stu = new Stu();
		stu.name = "Amaris";
		Computer c = new Computer();
		c.brand = "ASUS";
		stu.comp = c;
		stu.study();
	}
}
class Computer{
	String brand;
}
```
![result](https://img-blog.csdnimg.cn/20200219164256671.png)
# 4.4 面向对象的内存分析
- Java 虚拟机的内存可以分为三个区域：**栈stack**、**堆heap**以及**方法区method area**
- **栈的特点**
1. 栈描述的是**方法**执行的内存模型。每个方法被调用都会创建一个栈帧(存储局部变量、操作数、方法出口等)

2. JVM为每个线程创建一个栈，用于存放该线程执行方法的信息(实际参数、局部变量等)

3. 栈属于**线程私有**，不能实现线程间的共享!

4. 栈的存储特性是“先进后出，后进先出”

5. 栈是由系统自动分配，速度快!栈是一个**连续**的内存空间!
- **堆的特点**
1. 堆用于存储创建好的**对象和数组**(数组也是对象)

2. JVM只有一个堆，被**所有线程共享**

3. 堆是一个**不连续**的内存空间，分配灵活，速度慢!
- **方法区(又叫静态区)特点**
1. JVM只有一个方法区，被所有线程共享!

2. 方法区实际也是堆，只是用于**存储类、常量**相关的信息!
3. 用来存放程序中永远是不变或唯一的内容。(类信息【Class对象】、静态变量、字符串常量等)

![内存分配图](https://img-blog.csdnimg.cn/20200219170021500.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![内存分配图](https://img-blog.csdnimg.cn/20200219170036646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 4.5 构造方法
- 构造器也叫构造方法(constructor)，用于**对象的初始化**。（ init )
- 构造器是一个创建对象时被自动调用的特殊方法，目的是对象的初始化。
- 构造器的名称应与类的名称一致。
- Java通过new关键字来调用构造器，从而返回该类的实例，是一种特殊的方法。

```java
class Point{
	double x,y;
	
	public Point(double _x,double _y) {
		x = _x;
		y = _y;
	}
	
	public double getDistance(Point p) {
		return Math.sqrt((x-p.x)*(x-p.x) + (y-p.y)*(y-p.y));
	}
}
public class Test {
	public static void main(String[] arg) {
		Point p = new Point(3,4);
		Point q = new Point(0,0);
		System.out.println(p.getDistance(q));
	}
}
```
# 4.6 构造方法的重载
- 　　构造方法也是方法，只不过有特殊的作用而已。与普通方法一样，构造方法也可以重载。
- 如果方法构造中形参名与属性名相同时，需要使用**this**关键字区分属性与形参。

　　this.id 表示属性id;id表示形参id
```java
public class User{
	int id;
	String name;
	String pwd;
	
	public User(int id,String name) {
		//super();
		this.id = id;
		this.name = name;
	}
	public User(int id,String name,String pwd) {
		this.id = id;
		this.name = name;
		this.pwd = pwd;
	}
	public static void main(String[] arg) {
		User u1 = new User(24,"Amaris");
		User u2 = new User(24,"Amaris","7851");
	}
}
```
# 4.7 垃圾回收机制
- $Garbage\ Collection$
- 　Java引入了**垃圾回收机制**，令C++程序员最头疼的内存管理问题迎刃而解。
- Java程序员可以将更多的精力放到业务逻辑上而不是内存管理工作上，大大的提高了开发效率。
## 4.7.1 垃圾回收原理和算法
- **内存管理**
1. Java的内存管理很大程度指的就是对象的管理，其中包括对象空间的分配和释放。
2. 对象空间的分配：使用new关键字创建对象即可
3. 对象空间的释放：将对象赋值null即可。垃圾回收器将负责回收所有”不可达”对象的内存空间。
- **垃圾回收过程**
1. 发现无用的对象
2.  回收无用对象占用的内存空间。
- 垃圾回收机制保证可以将“无用的对象”进行回收。无用的对象指的就是没有任何变量引用该对象。Java的垃圾回收器通过相关算法发现无用对象，并进行清除和整理。
- **垃圾回收相关算法**
1. 引用计数法
堆中每个对象都有一个引用计数。被引用一次，计数加1. 被引用变量值变为null，则计数减1，直到计数为0，则表示变成无用对象。优点是算法简单，缺点是“循环引用的无用对象”无法别识别。
![循环引用示例](https://img-blog.csdnimg.cn/20200219202428203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
2.  引用可达法(根搜索算法) 
程序把所有的引用关系看作一张图，从一个节点GC ROOT开始，寻找对应的引用节点，找到这个节点以后，继续寻找这个节点的引用节点，当所有的引用节点寻找完毕之后，剩余的节点则被认为是没有被引用到的节点，即无用的节点。
## 4.7.2 通用的分代垃圾回收机制
- **分代垃圾回收机制**，是基于这样一个事实：不同的对象的生命周期是不一样的。因此，不同生命周期的对象可以采取不同的回收算法，以便提高回收效率。我们将对象分为三种状态：年轻代、年老代、持久代。**JVM将堆内存划分为 Eden、Survivor 和 Tenured/Old 空间。**
1. **年轻代**
所有新生成的对象首先都是放在**Eden区**。 年轻代的目标就是尽可能快速的收集掉那些生命周期短的对象，对应的是Minor GC，每次 Minor GC 会清理年轻代的内存，算法采用效率较高的复制算法，频繁的操作，但是会浪费内存空间。当“年轻代”区域存放满对象后，就将对象存放到年老代区域。

2. **年老代**
在年轻代中经历了N(默认15)次垃圾回收后仍然存活的对象，就会被放到年老代中。因此，可以认为年老代中存放的都是一些生命周期较长的对象。年老代对象越来越多，我们就需要启动Major GC和Full GC(全量回收)，来一次大扫除，全面清理年轻代区域和年老代区域。

3. **持久代**
用于存放静态文件，如Java类、方法等。持久代对垃圾回收没有显著影响。


-  **GC垃圾收集器**
1. **Minor GC**
用于清理年轻代区域。Eden区满了就会触发一次Minor GC。清理无用对象，将有用对象复制到“Survivor1”、“Survivor2”区中(这两个区，大小空间也相同，同一时刻Survivor1和Survivor2只有一个在用，一个为空)

5. **Major GC**
用于清理老年代区域。

6. **Full GC**
用于清理年轻代、年老代区域。 成本较高，会对系统性能产生影响。
- **垃圾回收过程**
1. 新创建的对象，绝大多数都会存储在Eden中，

8. 当Eden满了（达到一定比例）不能创建新对象，则触发垃圾回收（GC），将无用对象清理掉， 然后剩余对象复制到某个Survivor中，如S1，同时清空Eden区

9. 当Eden区再次满了，会将S1中的不能清空的对象存到另外一个Survivor中，如S2，同时将Eden区中的不能清空的对象，也复制到S1中，保证Eden和S1，均被清空。

10. 重复多次(默认15次)Survivor中没有被清理的对象，则会复制到老年代Old(Tenured)区中，

11. 当Old区满了，则会触发一个一次完整地垃圾回收（FullGC），之前新生代的垃圾回收称为（minorGC）
![通用的分代垃圾回收机制](https://img-blog.csdnimg.cn/20200219203227776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 4.7.3 JVM 调优和 Full GC
- 在对JVM调优的过程中，很大一部分工作就是对于Full GC的调节。有如下原因可能导致Full GC：

1. 年老代(Tenured)被写满

2. 持久代(Perm)被写满

3. System.gc()被显式调用（程序建议GC启动，不是调用GC）

4. 上一次GC之后Heap的各域分配策略动态变化
## 4.7.4 开发中容易造成内存泄漏的操作
- **创建大量无用对象**
比如，我们在需要大量拼接字符串时，使用了String而不是StringBuilder。
![创建大量无用对象](https://img-blog.csdnimg.cn/2020021920454434.png)
- **静态集合类的使用**
像HashMap、Vector、List等的使用最容易出现内存泄露，这些静态变量的生命周期和应用程序一致，所有的对象Object也不能被释放。
- **各种连接对象(IO流对象、数据库连接对象、网络连接对象)未关闭**
IO流对象、数据库连接对象、网络连接对象等连接对象属于物理连接，和硬盘或者网络连接，不使用的时候一定要关闭。
- **监听器的使用**
释放对象时，没有删除相应的监听器。
- **要点**
1. 程序员无权调用垃圾回收器。

2. 程序员可以调用System.gc()，该方法只是通知JVM，并不是运行垃圾回收器。尽量少用，会申请启动Full GC，成本高，影响系统性能。

3.  finalize方法，是Java提供给程序员用来释放对象或资源的方法，但是尽量少用。
# 4.8 this 关键字
- **this的本质就是“创建好的对象的地址”**! 由于在构造方法调用前，对象已经创建。因此，在构造方法中也可以使用this代表“当前对象” 。
1.  在程序中产生二义性之处，应使用this来指明当前对象;普通方法中，this总是指向调用该方法的对象。构造方法中，this总是指向正要初始化的对象。

2.  使用this关键字**调用重载**的构造方法，避免相同的初始化代码。但只能在构造方法中用，并且**必须位于构造方法的第一句**。
![this关键字调用重载的构造方法](https://img-blog.csdnimg.cn/20200219205609890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
3. **this不能用于static方法中。**
# 4.9 static 关键字
- 在类中，用**static声明的成员变量**为**静态成员变量**，也称为**类变量**。（公有的） 类变量的生命周期和类相同，在整个应用程序执行期间都有效。它有如下特点：
1. 为该类的公用变量，属于类，被该类的所有实例共享，在类被载入时被显式初始化。

2. 对于该类的所有对象来说，static成员变量只有一份。被该类的所有对象共享!!

3.  一般用“类名.类属性/方法”来调用。(也可以通过对象引用或类名(不需要实例化)访问静态成员。)

4.  在static方法中不可直接访问非static的成员。

```java
/**
 * 测试static关键字的用法
 * @author 高淇
 *
 */
public class User2 {
    int id; // id
    String name; // 账户名
    String pwd; // 密码
     
    static String company = "北京尚学堂"; // 公司名称
     
     
    public User2(int id, String name) {
        this.id = id;
        this.name = name;
    }
     
    public void login() {
        printCompany();
        System.out.println(company); 
        System.out.println("登录：" + name);
    }
     
    public static void printCompany() {
//         login();//调用非静态成员，编译就会报错
        System.out.println(company);
    }
     
    public static void main(String[] args) {
        User2 u = new User2(101, "高小七");
        User2.company = "test";
        User2.printCompany();
        User2.company = "北京阿里爷爷";
        User2.printCompany();
    }
}
```
# 4.10 静态初始化块
- 构造方法用于对象的初始化!**静态初始化块，用于类的初始化操作**!在静态初始化块中不能直接访问非static成员。
- **静态初始化块执行顺序**
1. 上溯到Object类，先执行Object的静态初始化块，再向下执行子类的静态初始化块，直到我们的类的静态初始化块为止。
2. 构造方法执行顺序和上面顺序一样!!

```java
public class User3 {
    int id;        //id
    String name;   //账户名
    String pwd;   //密码
    static String company; //公司名称
    static {
        System.out.println("执行类的初始化工作");
        company = "北京尚学堂";
        printCompany();
    }  
    public static void printCompany(){
        System.out.println(company);
    }  
    public static void main(String[] args) {
        User3  u3 = new User3();
    }
}
```
# 4.11 参数传值机制
- **基本数据类型参数的传值**
传递的是值的副本。 副本改变不会影响原件。

- **引用类型参数的传值**
传递的是值的副本。但是引用类型指的是“对象的地址”。因此，副本和原参数都指向了同一个“地址”，改变“副本指向地址对象的值，也意味着原参数指向对象的值也发生了改变”。（**对象是一个地址**）

```java
public class User4 {
    int id;        //id
    String name;   //账户名
    String pwd;   //密码
       
    public User4(int id, String name) {
        this.id = id;
        this.name = name;
    }
      
    public   void   testParameterTransfer01(User4  u){
        u.name="高小八";
    }
     
    public   void   testParameterTransfer02(User4  u){
        u = new  User4(200,"高三");//地址改变了
    }
      
    public static void main(String[] args) {
        User4   u1  =  new User4(100, "高小七");
         
        u1.testParameterTransfer01(u1); 
        System.out.println(u1.name);//地址未变，
 
        u1.testParameterTransfer02(u1);
        System.out.println(u1.name);//新建了对象，地址改变
    }
}
```
![result](https://img-blog.csdnimg.cn/20200219212130414.png)
# 4.12 包
- **包机制**是Java中管理类的重要手段。 开发中，我们会遇到大量同名的类，通过包我们很容易对解决类重名的问题，也可以实现对类的有效管理。 包对于类，相当于文件夹对于文件的作用。
# 4.13 package
- 通常是类的第一句非注释性语句。

- 包名：域名倒着写即可，再加上模块名，便于内部管理类。
![包名](https://img-blog.csdnimg.cn/20200219212906675.png)
- 写项目时都要加包，不要使用默认包。

- com.gao和com.gao.car，这两个包没有包含关系，是两个完全独立的包。只是逻辑上看起来后者是前者的一部分。
![package的使用](https://img-blog.csdnimg.cn/20200219213015185.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 4.13.1 JDK 中的包

![JDK中的包](https://img-blog.csdnimg.cn/20200219213411452.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 4.13.2 导入类 import
1. Java会默认导入java.lang包下所有的类，因此这些类我们可以直接使用。

2. 如果导入两个同名的类，只能用包名+类名来显示调用相关类：　
## 4.13.3 静态导入
-  **静态导入(static import)** 是在JDK1.5新增加的功能，其作用是用于导入指定类的静态属性，这样我们可以直接使用静态属性。
![静态导入](https://img-blog.csdnimg.cn/20200219214555911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 4.14 总结
1. 面向对象可以帮助我们从宏观上把握、从整体上分析整个系统。 但是具体到实现部分的微观操作(就是一个个方法)，仍然需要面向过程的思路去处理。

2. 类可以看成一类对象的模板，对象可以看成该类的一个具体实例。

3. 对于一个类来说，一般有三种常见的成员：属性field、方法method、构造器constructor。

4.  构造器也叫构造方法，用于对象的初始化。构造器是一个创建对象时被自动调用的特殊方法，目的是对象的初始化。构造器的名称应与类的名称一致。

5. Java引入了垃圾回收机制，令C++程序员最头疼的内存管理问题迎刃而解。Java程序员可将更多的精力放到业务逻辑上而不是内存管理工作，大大提高开发效率。
6. this的本质就是“创建好的对象的地址”! this不能用于static方法中。

7.  在类中，用static声明的成员变量为静态成员变量，也称为类变量。类变量的生命周期和类相同，在整个应用程序执行期间都有效。在static方法中不可直接访问非static的成员。

8. Java方法中所有参数都是“值传递”，也就是“传递的是值的副本”。也就是说，我们得到的是“原参数的复印件，而不是原件”。因此，复印件改变不会影响原件。

9.  通过package实现对类的管理;如果我们要使用其他包的类，需要使用import导入，从而可以在本类中直接通过类名来调用。
