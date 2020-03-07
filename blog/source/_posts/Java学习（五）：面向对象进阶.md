---
title: Java学习（五）：面向对象进阶
date: 2020-02-20 22:02:55
tags:
	- Java
---
# 5.1 概述
- 本章重点针对面向对象的三大特征：**继承**、**封装**、**多态**进行详细的讲解。另外还包括**抽象类**、**接口**、**内部类**等概念。
## 5.1.1 继承的实现
- $inheritance$ [ɪnˈherɪtəns]
-  **继承**让我们更加容易实现类的扩展。
<!--more-->
- **extends**的意思是“扩展”。子类是父类的扩展。
## 5.1.2 instanceof 运算符
-  **instanceof** 是二元运算符，左边是对象，右边是类
- 当对象是右面类或子类所创建对象时，返回true；否则，返回false。
![instanceof 运算符](https://img-blog.csdnimg.cn/20200220111100390.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 5.1.3 继承的使用要点
1. 父类也称作超类、基类、派生类等。

2. Java中只有**单继承**，没有像C++那样的多继承。多继承会引起混乱，使得继承链过于复杂，系统难于维护。

3. Java中类没有多继承，**接口有多继承**。

4. 子类继承父类，可以得到父类的全部属性和方法 (除了父类的构造方法)，但不见得可以直接访问(比如，父类私有的属性和方法)。

5. 如果定义一个类时，没有调用extends，则它的父类是：java.lang.Object。
## 5.1.4 方法的重写（override）
-  子类通过重写父类的方法，可以用自身的行为替换父类的行为
- **方法的重写**是实现多态的必要条件。
- 重写要点
1. “==”： 方法名、形参列表相同。

2. “≤”：返回值类型和声明异常类型，子类小于等于父类。

3. “≥”： 访问权限，子类大于等于父类。
```java
package cn.amaris.oo2;

public class TestExtends {
	public static void main(String[] args) {
		Student s1 = new Student();
		s1.study();
		s1.rest();
		Student s2 = new Student("Amaris",172,"CS");
		System.out.println(s2 instanceof Student);
	}

}

class Person{
	String name;
	int height;
	
	public void rest() {
		System.out.println("resting...");
	}
	
}

class Student extends Person{
	String major;
	
	public Student(String name,int height,String major) {
		this.name = name;
		this.height = height;
		this.major = major;
	}
	public Student() {  //空构造器，重载
		
	}
	
	public void rest() {  // 方法的重写
		System.out.println("Listening...");
	}
	public void study() {
		System.out.println("studying...");
	}
}
```
# 5.2 Object 类
## 5.2.1 Object 类基本特性
- **Object**类是所有Java类的根基类，也就意味着所有的Java对象都拥有Object类的属性和方法。
- 如果在类的声明中未使用extends关键字指明其父类，则默认继承Object类。
## 5.2.2 toString 方法
-   Object类中定义有public String toString()方法，其返回值是 String 类型。
![src_toString](https://img-blog.csdnimg.cn/20200220114301906.png)
 -   根据如上源码得知，默认会返回“类名+@+16进制的hashcode”。在打印输出或者用字符串连接对象时，会自动调用该对象的toString()方法。
 - Object的hashCode()默认是返回内存地址的，但是hashCode()可以重写，所以hashCode()不能代表内存地址的不同
- System.identityHashCode(Object)方法可以返回对象的内存地址,不管该对象的类是否重写了hashCode()方法


```java
package cn.amaris.oo2;

public class TestToString {
	public static void main(String[] args) {
		TestToString t = new TestToString();
		System.out.println(t.toString());
		System.out.println(t);
	}
	 public String toString() {  //重写
	        return "test toString";
	    }

}
```
## 5.2.3 == 和 equals 方法
- “==”代表比较双方是否相同。如果是基本类型则表示值相等，如果是引用类型则表示地址相等即是同一个对象。
-   Object类中定义有：public boolean equals(Object obj)方法，提供定义“对象内容相等”的逻辑。
-  Object 的 equals 方法默认就是比较两个对象的**hashcode**，是同一个对象的引用时返回 true 否则返回 false。
![equals](https://img-blog.csdnimg.cn/20200220120213343.png)
- 重写前
```java
package cn.amaris.oo2;

public class TestEquals {
	public static void main(String[] args) {
		Object obj;
		String str;
		
		User u1 = new User(24,"A","123456");
		User u2 = new User(24,"A","123456");
		
		System.out.println(u1 == u2);
		System.out.println(u1.equals(u2));
	}

}

class User {
	int id;
	String name;
	String pwd;

	public User(int id, String name, String pwd) {
		super();
		this.id = id;
		this.name = name;
		this.pwd = pwd;
	}

}
```
![result](https://img-blog.csdnimg.cn/20200220121406994.png)
- 重写后
```java
package cn.amaris.oo2;

public class TestEquals {
	public static void main(String[] args) {
		Object obj;
		String str;
		
		User u1 = new User(24,"A","123456");
		User u2 = new User(24,"A","123456");
		
		System.out.println(u1 == u2);
		System.out.println(u1.equals(u2));
	}

}

class User {
	int id;
	String name;
	String pwd;

	public User(int id, String name, String pwd) {
		super();
		this.id = id;
		this.name = name;
		this.pwd = pwd;
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + id;
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		User other = (User) obj;
		if (id != other.id)
			return false;
		return true;
	}
}
```
![result](https://img-blog.csdnimg.cn/20200220122125188.png)
# 5.3 super关键字与继承树追溯
## 5.3.1 super 关键字
- super是直接父类对象的引用。可以通过super来访问父类中被子类覆盖的方法或属性。
- 使用super调用普通方法，语句没有位置限制，可以在子类中随便调用。
- 若是构造方法的第一行代码没有显式的调用super(...)或者this(...);那么Java默认都会调用super(),含义是调用父类的无参数构造方法。这里的super()可以省略。

```java
public class TestSuper01 { 
    public static void main(String[] args) {
        new ChildClass().f();
    }
}
class FatherClass {
    public int value;
    public void f(){
        value = 100;
        System.out.println ("FatherClass.value="+value);
    }
}
class ChildClass extends FatherClass {
    public int value;
    public void f() {
        super.f();  //调用父类对象的普通方法
        value = 200;
        System.out.println("ChildClass.value="+value);
        System.out.println(value);
        System.out.println(super.value); //调用父类对象的成员变量
    }
}
```
## 5.3.2 继承树追溯 
- **属性/方法查找顺序**(比如：查找变量h)
1. 查找当前类中有没有属性h

2. 依次上溯每个父类，查看每个父类中是否有h，直到Object

3. 如果没找到，则出现编译错误。

4. 上面步骤，只要找到h变量，则这个过程终止。
- **构造方法调用顺序**
  构造方法第一句总是：super(…)来调用父类对应的构造方法。所以，流程就是：先向上追溯到Object，然后再依次向下执行类的初始化块和构造方法，直到当前子类为止。

      注：静态初始化块调用顺序，与构造方法调用顺序一样，不再重复。
```java
public class TestSuper02 { 
    public static void main(String[] args) {
        System.out.println("开始创建一个ChildClass对象......");
        new ChildClass();
    }
}
class FatherClass {
    public FatherClass() {
        System.out.println("创建FatherClass");
    }
}
class ChildClass extends FatherClass {
    public ChildClass() {
        System.out.println("创建ChildClass");
    }
}
```
![result](https://img-blog.csdnimg.cn/20200220123514543.png)
# 5.4 封装
- $capsulation$ [kæpsju'leiʃən]
## 5.4.1 封装的作用和含义
- **封装**就是把对象的属性和操作结合为一个独立的整体，并尽可能隐藏对象的内部实现细节。
- 需要让用户知道的才暴露出来，不需要让用户知道的全部隐藏起来，这就是封装。
## 5.4.2 封装的实现—使用访问控制符
-    Java是使用“访问控制符”来控制哪些细节需要封装，哪些细节需要暴露的。
-  Java中4种“访问控制符”分别为**private**、**default**、**protected**、**public**，它们说明了面向对象的封装性，所以我们要利用它们尽可能的让访问权限降到最低，从而提高安全性。
![访问权限修饰符](https://img-blog.csdnimg.cn/20200220200229431.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
1.  **private** 表示私有，只有**自己类**能访问

2.  **default** 表示没有修饰符修饰，只有**同一个包的类**能访问

3. **protected** 表示可以被**同一个包的类以及其他包中的子类**访问

4. **public** 表示可以被该项目的**所有包中的所有类**访问

```java
package cn.amaris.oo2;

public class Human{
	private int age;
	public String name;
	protected int height;
	void sayAge() {
		System.out.println(age);
	}
}

class Boy extends Human{
	void sayHello() {
		System.out.println(height);  //  age,private
	}
}
```

```java
package cn.amaris.oo3;

import cn.amaris.oo2.*;

public class TestEncapsulation2 {
	public static void main(String[] args) {
		Human h2 = new Human();
		h2.name = "Jorge";
		
		Girl b1 = new Girl();
	}
}

class Girl extends Human{
	void sayHello() {
		System.out.println(height);  //  age,private
	}
}
```
## 5.4.3 封装的使用细节
- **类的属性的处理**
1.  一般**使用private访问权限**。

2.  **提供相应的get/set方法来访问相关属性**，这些方法通常是public修饰的，以提供对属性的赋值与读取操作(注意：boolean变量的get方法是is开头!)。（右键->source->set/get...自动生成）

3. 一些只用于**本类的辅助性方法**可以用**private**修饰，**希望其他类调用的方法**用**public**修饰。（通常 public）

```java
package cn.amaris.oo3;

public class Person {
	private int id;
	private String name;
	private int age;
	private boolean man;
	
	public void setName(String name) {
		this.name = name;
	}
	
	public String getName(){
		return this.name;
	}
	
	public void setAge(int age) {
		if(age>=0&&age<=130) {
			this.age = age;
		}else {
			System.out.println("Error age!");
		}
	}
	
	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public boolean isMan() {
		return man;
	}

	public void setMan(boolean man) {
		this.man = man;
	}

	public int getAge() {
		return this.age;
	}
	
}
```

```java
package cn.amaris.oo2;

import cn.amaris.oo3.*;

public class Human{
	public static void main(String[] args) {
		Person p1 = new Person();
		p1.setName("Amaris");
		p1.setAge(20);
		
		System.out.println(p1.getAge());
		System.out.println(p1.getName());
	}
}
```
# 5.5 多态
- $polymorphism$ [,pɒlɪ'mɔːfɪz(ə)m]
- **多态**指的是同一个方法调用，由于对象不同可能会有不同的行为。现实生活中，同一个方法，具体实现会完全不同。
- 多态使得免于繁杂的方法重载
1. 多态是方法的多态，不是属性的多态(多态与属性无关)。
2. 多态的存在要有**3个必要条件**：**继承**，**方法重写**，**父类引用指向子类对象**。
3. 父类引用指向子类对象后，用该父类引用调用子类重写的方法，此时多态就出现了。
# 5.6 对象的转型
- 父类引用指向子类对象，我们称这个过程为**向上转型**，属于自动类型转换。
向上转型时,**父类只能调用父类方法或者子类覆写后的方法**,而子类中的单独方法则是无法调用的
- 向上转型后的父类引用变量只能调用它编译类型的方法，不能调用它运行时类型的方法。这时，我们就需要进行类型的强制转换，我们称之为**向下转型**!
![对象的转型](https://img-blog.csdnimg.cn/20200220212431863.png)
# 5.7 final 关键字
1.  **修饰变量**: 被他修饰的变量不可改变。一旦赋了初值，就不能被重新赋值。
![修饰变量](https://img-blog.csdnimg.cn/20200220213500636.png)
2. **修饰方法**：该方法不可被子类重写。但是可以被重载!
![修饰方法](https://img-blog.csdnimg.cn/20200220213533248.png)
3.  **修饰类**: 修饰的类不能被继承。比如：Math、String等。
![修饰类](https://img-blog.csdnimg.cn/20200220213607204.png)
# 5.8 抽象方法和抽象类
- **抽象方法**
   使用**abstract**修饰的方法，没有方法体，**只有声明**。定义的是一种“规范”，就是告诉子类必须要给抽象方法提供具体的实现。
- **抽象类**
包含抽象方法的类就是**抽象类**。通过**abstract**方法定义规范，然后**要求子类必须定义具体实现**。通过抽象类，我们就可以做到严格限制子类的设计，使子类之间更加通用。（只可以new子类，相当于给子类提供模板）
- **抽象类的使用要点**
1. 有抽象方法的类只能定义成抽象类

2.  抽象类不能实例化，即不能用new来实例化抽象类。

3. 抽象类可以包含属性、方法、构造方法。但是构造方法不能用来new实例，只能用来被子类调用。

4. 抽象类只能用来被继承。

5. 抽象方法必须被子类实现。

```java
package cn.amaris.proj0501;

abstract public class TestAbstract {
	public static void main(String[] args) {
		Dog d = new Dog();
		d.shout();
	}
}

abstract class Animal {
	abstract public void shout();
	
	public void run() {
		System.out.println("Runing...");
	}

}

class Dog extends Animal{
	public void shout() {
		System.out.println("wang.wang.wang...");
	}
}
```
# 5.9 接口
- **接口**就是比“抽象类”还“抽象”的“抽象类”，可以更加规范的对子类进行约束。全面地专业地实现了：规范和具体实现的分离。
-  抽象类还提供某些具体实现，接口不提供任何实现，接口中所有方法都是抽象方法。接口是完全**面向规范的**，规定了一批类具有的公共方法规范。
## 5.9.1 接口的作用
- 从接口的实现者角度看，接口定义了可以向外部提供的服务。

- 从接口的调用者角度看，接口定义了实现者能提供那些服务。

-  **接口是两个模块之间通信的标准，通信的规范。**如果能把你要设计的模块之间的接口定义好，就相当于完成了系统的设计大纲，剩下的就是添砖加瓦的具体实现了。大家在工作以后，做系统时往往就是使用“面向接口”的思想来设计系统。

- **接口和实现类不是父子关系，是实现规则的关系。**比如：我定义一个接口Runnable，Car实现它就能在地上跑，Train实现它也能在地上跑，飞机实现它也能在地上跑。就是说，如果它是交通工具，就一定能跑，但是一定要实现Runnable接口。
- ** 接口的本质探讨**
 接口就是规范，定义的是一组规则，体现了现实世界中“如果你是…则必须能…”的思想。如果你是天使，则必须能飞。如果你是汽车，则必须能跑。如果你是好人，则必须能干掉坏人;如果你是坏人，则必须欺负好人。
接口的本质是契约，就像我们人间的法律一样。制定好后大家都遵守。
面向对象的精髓，是对对象的抽象，最能体现这一点的就是接口。为什么我们讨论设计模式都只针对具备了抽象能力的语言(比如C++、Java、C#等)，就是因为设计模式所研究的，实际上就是如何合理的去抽象。
- **区别**
1. 普通类：具体实现

2. 抽象类：具体实现，规范(抽象方法)

3. 接口：规范!
## 5.9.2 定义和使用接口
- **声明格式**
![声明格式](https://img-blog.csdnimg.cn/20200222195243514.png)
- **定义接口的详细说明**

1.  访问修饰符：只能是public或默认。

2. 接口名：和类名采用相同命名机制。

3.  extends：**接口可以多继承**。（普通类只有单继承）
 接口完全支持多继承。和类的继承类似，子接口扩展某个父接口，将会获得父接口中所定义的一切。
4. 常量：接口中的属性只能是常量，总是：public static final 修饰。不写也是。

5. 方法：接口中的方法只能是：public abstract。 省略的话，也是public abstract。

- **要点**

1. 子类通过**implements**来实现接口中的规范。
2. 接口不能创建实例，但是可用于声明引用变量类型。
3. 一个类实现了接口，必须实现接口中所有的方法，并且这些方法只能是public的。
4. JDK1.7之前，接口中只能包含静态常量、抽象方法，不能有普通属性、构造方法、普通方法。
5.  JDK1.8后，接口中包含普通的静态方法。

```java
package cn.amaris.proj0501;

public interface MyInterface {
	int MAX_AGE = 130;
	
	void test01();
	public static void main(String[] args) {
		SubInterface s = new SubInterface();
		s.test01();
	}

}

class SubInterface implements MyInterface{
	public void test01() {
		System.out.println("test SubInterface!");
	}
}
```

```java
package cn.amaris.proj0501;

public class TestMyinterface {
	public static void main(String[] args) {
		Angel a = new Angel();
		a.fly();
		a.helpOther();
	}

}

interface Volant{
	int FLY_HEIGHT = 1000;
	void fly();
}

interface Honest{
	void helpOther();
}

class Angel implements Volant,Honest{
	

	@Override
	public void helpOther() {
		System.out.println("Helping...");
		
	}

	@Override
	public void fly() {
		System.out.println("Flying...");
		
	}
	
}
```
## 5.9.3 面向接口编程
- 面向接口编程是面向对象编程的一部分。

- 软件设计中最难处理的就是需求的复杂变化，需求的变化更多的体现在具体实现上。

- 通过面向接口编程，而不是面向实现类编程，可以大大降低程序模块间的耦合性，提高整个系统的可扩展性和和可维护性。

-  面向接口编程的概念比接口本身的概念要大得多。设计阶段相对比较困难，在你没有写实现时就要想好接口，接口一变就乱套了，所以设计要比实现难!
# 5.10 内部类
## 5.10.1 内部类的概念
-  一般情况，我们把类定义成独立的单元。有些情况下，我们把一个类放在另一个类的内部定义，称为**内部类**(innerclasses)。
-    内部类可以使用public、default、protected 、private以及static修饰。而外部顶级类(我们以前接触的类)只能使用public和default修饰。
-   内部类只是一个编译时概念，一旦我们编译成功，就会成为完全不同的两个类。对于一个名为Outer的外部类和其内部定义的名为Inner的内部类。编译完成后会出现Outer.class和Outer$Inner.class两个类的字节码文件。所以内部类是相对独立的一种存在，其成员变量/方法名可以和外部类的相同。
- **内部类的作用**

1. 内部类提供了更好的封装。只能让外部类直接访问，不允许同一个包中的其他类直接访问。
2. 内部类**可以直接访问外部类的私有属性**，内部类被当成其外部类的成员。 但外部类不能访问内部类的内部属性。

3. 接口只是解决了多重继承的部分问题，而内部类使得多重继承的解决方案变得更加完整。

- **内部类的使用场合**
4. 由于内部类提供了更好的封装特性，并且可以很方便的访问外部类的属性。所以，**在只为外部类提供服务的情况下可以优先考虑使用内部类**。
5. 使用内部类间接实现多继承：每个内部类都能独立地继承一个类或者实现某些接口，所以无论外部类是否已经继承了某个类或者实现了某些接口，对于内部类没有任何影响。
## 5.10.2 内部类的分类
- 在Java中内部类主要分为**成员内部类**(非静态内部类、静态内部类)、**匿名内部类**、**局部内部类**。
- **非静态内部类**
外部类里使用非静态内部类和平时使用其他类没什么不同

1. 非静态内部类必须寄存在一个外部类对象里。因此，如果有一个非静态内部类对象那么一定存在对应的外部类对象。非静态内部类对象单独属于外部类的某个对象。

2. 非静态内部类可以直接访问外部类的成员，但是外部类不能直接访问非静态内部类成员。
3. 非静态内部类不能有静态方法、静态属性和静态初始化块。

4. 外部类的静态方法、静态代码块不能访问非静态内部类，包括不能使用非静态内部类定义变量、创建实例。

5. 成员变量访问要点：

        a. 内部类里方法的局部变量：变量名。
    
        b. 内部类属性：this.变量名。
    
        c. 外部类属性：外部类名.this.变量名。
    


```java
package cn.amaris.proj0501;

public class TestInnerClass {
	public static void main(String[] args) {
		
		//创建内部类对象
		Outer.Inner inner = new Outer().new Inner();
		inner.show();
	}

}

class Outer{
	private int age = 10;
	public void testOuter() {
		System.out.println("test outer...");
	}
	
	class Inner{
		int age = 20;
		public void show() {
			int age = 30;
			System.out.println("外部类的成员变量 age: "+Outer.this.age);
			System.out.println("内部类的成员变量 age: "+this.age);
			System.out.println("局部变量 age: "+age);
		}
	}
}
```
![result](https://img-blog.csdnimg.cn/20200222204644156.png)
- **静态内部类**
1. 定义方式：
![定义方式](https://img-blog.csdnimg.cn/20200222205006578.png)

2. 使用要点：

       a. 当一个静态内部类对象存在，并不一定存在对应的外部类对象。
        因此，静态内部类的实例方法不能直接访问外部类的实例方法。
    
       b. 静态内部类看做外部类的一个静态成员。 因此，外部类的方法
       中可以通过：“静态内部类.名字”的方式访问静态内部类的静态成
       员，通过 new 静态内部类()访问静态内部类的实例。
   


```java
package cn.amaris.proj0501;

public class TestStaticInner {
	public static void main(String[] args) {
		Outer2.Inner2 inner = new Outer2.Inner2();
		inner.test2();
	}

}

class Outer2{
	static class Inner2{
		public void test2() {
			System.out.println("test static inner2...");
		}
	}
}
```
- **匿名内部类**
 适合那种只需要使用一次的类。比如：键盘监听操作等等。（桌面编程会用）
1.  匿名内部类没有访问修饰符。
2. 匿名内部类没有构造方法。因为它连名字都没有那又何来构造方法呢。![匿名内部类](https://img-blog.csdnimg.cn/20200222205452419.png)


```java
package cn.amaris.proj0501;

public class TestAnonymousInnerClass {
	public static void test01(C1 c) {
		c.testc1();
	}
	
	public static void main(String[] args) {
		TestAnonymousInnerClass.test01(new C1() {

			@Override
			public void testc1() {
				System.out.println("test anonymousInnerClass...");
				
			}
			
		});
	}

}

interface C1{
	void testc1();
}
```
- **局部内部类**
还有一种内部类，它是定义在方法内部的，**作用域只限于本方法**，称为**局部内部类**。
 局部内部类的的使用主要是用来解决比较复杂的问题，想创建一个类来辅助我们的解决方案，到那时又不希望这个类是公共可用的，所以就产生了局部内部类。局部内部类和成员内部类一样被编译，只是它的作用域发生了改变，它只能在该方法中被使用，出了该方法就会失效。
 局部内部类在实际开发中应用很少。

# 5.11 String 类
## 5.11.1 String 基础
1. **String类**又称作**不可变字符序列**。
2. String位于**java.lang**包中，Java程序默认导入java.lang包下的所有类。
3. Java字符串就是**Unicode字符序列**，例如字符串“Java”就是4个Unicode字符’J’、’a’、’v’、’a’组成的。
4. Java没有内置的字符串类型，而是在标准Java类库中提供了一个预定义的类String，每个用双引号括起来的字符串都是String类的一个**实例**。
5.  n-符号**"+"**把两个字符串按给定的顺序连接在一起，并且是完全按照给定的形式。
6. n-当"+"运算符两侧的操作数中只要有一个是字符串(String)类型，系统会自动将另一个操作数转换为字符串然后再进行连接。
![example](https://img-blog.csdnimg.cn/20200222210613283.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![example](https://img-blog.csdnimg.cn/20200222210709542.png)
## 5.11.2 String类和常量池
[String类和常量池](https://www.sxt.cn/Java_jQuery_in_action/five-constant-pool.html)
1. **全局字符串常量池(String Pool)**

      全局字符串常量池中存放的内容是在类加载完成后存到String Pool中的，在每个VM中只有一份，存放的是字符串常量的引用值(在堆中生成字符串对象实例)。
      **字符串比较用equals**

2. **class文件常量池(Class Constant Pool)**

      class常量池是在编译的时候每个class都有的，在编译阶段，存放的是常量(文本字符串、final常量等)和符号引用。

3. **运行时常量池(Runtime Constant Pool)**

      运行时常量池是在类加载完成之后，将每个class常量池中的符号引用值转存到运行时常量池中，也就是说，每个class都有一个运行时常量池，类在解析之后，将符号引用替换成直接引用，与全局常量池中的引用值保持一致。
      
## 5.11.3 String类常用的方法
[Java SE Development Kit 8 Documentation](https://pan.baidu.com/s/1iekNMiGt-KzC0vFApZOvqQ)
提取码：h100
![String类常用的方法](https://img-blog.csdnimg.cn/20200222212614441.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 5.12 总结

- 高级语言可分为：面向过程和面向对象两大类

1.  面向过程与面向对象都是解决问题的思维方式，都是代码组织的方式。

2. 解决简单问题可以使用面向过程。

3. 解决复杂问题：宏观上使用面向对象把握，微观处理上仍然是面向过程。

- 对象和类的关系是特殊到一般，具体到抽象的关系。

- 栈内存

1. 每个线程私有，不能实现线程间的共享!

2. 局部变量放置于栈中。

3. 栈是由系统自动分配，速度快!栈是一个连续的内存空间!

- 堆内存

1. 放置new出来的对象!

2. 堆是一个不连续的内存空间，分配灵活，速度慢!

- 方法区

1. 被所有线程共享!

2. 用来存放程序中永远是不变或唯一的内容(类代码信息、静态变量、字符串常量)。

- 属性用于定义该类或该类对象包含的数据或者说静态属性。属性作用范围是整个类体。Java使用默认的值对其初始化。

- 方法则用于定义该类或该类实例的行为特征和功能实现。方法是类和对象行为特征的抽象。

- 构造器又叫做构造方法(constructor)，用于构造该类的实例。Java通过new关键字来调用构造方法，从而返回该类的实例，是一种特殊的方法。

- 垃圾回收机制

1. 程序员无权调用垃圾回收器。

2. 程序员可以通过System.gc()通知垃圾回收器(Garbage Collection，简称GC)运行，但是Java规范并不能保证立刻运行。

3. finalize方法，是Java提供给程序员用来释放对象或资源的方法，但是尽量少用。

- 方法的重载是指一个类中可以定义有相同的名字，但参数不同的多个方法。 调用时，会根据不同的参数表选择对应的方法。

- this关键字的作用

1. 让类中的一个方法，访问该类的另一个方法或属性。

2.  使用this关键字调用重载构造方法，可以避免相同的初始化代码，只能在构造方法中用，并且必须位于构造方法的第一句。

- static关键字

1.  在类中，用static声明的成员变量为静态成员变量，也称为类变量。

2.  用static声明的方法为静态方法。

3.  可以通过对象引用或类名(不需要实例化)访问静态成员。

- package的作用

1. 可以解决类之间的重名问题。

2. 便于管理类：合适的类位于合适的包!

- impport的作用
通过import可以导入其他包下面的类，从而可以在本类中直接通过类名来调用。

- super关键字的作用
super是直接父类对象的引用。可以通过super来访问父类中被子类覆盖的方法或属性。

- 面向对象的三大特征:继承、封装、多态。

- Object类是所有Java类的根基类。

- 访问权限控制符：范围由小到大分别是private、default、protected、public。

- 引用变量名 instanceof 类名 来判断该引用类型变量所“指向”的对象是否属于该类或该类的子类。

- final关键字可以修饰变量、修饰方法、修饰类。

- 抽象类是一种模版模式。抽象类为所有子类提供了一个通用模版，子类可以在这个模版基础上进行扩展，使用abstract修饰。

-  使用abstract修饰的方法为抽象方法必须被子类实现，除非子类也是抽象类。

- 使用interface声明接口

1. 从接口的实现者角度看，接口定义了可以向外部提供的服务。

2. 从接口的调用者角度看，接口定义了实现者能提供哪些服务。

- 内部类分为成员内部类、匿名内部类和局部内部类。

- String位于java.lang包中，Java程序默认导入java.lang包。

- 字符串的比较"=="与equals()方法的区别。
