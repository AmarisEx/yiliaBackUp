---
title: Java学习（六）：异常机制
date: 2020-02-27 10:43:03
tags:
	- Java
---
# 6.1 导引问题
- **异常处理**(Exception Handling)就是一种解决这一问题的机制，能够较好地处理程序不能正常运行的情况。
![example](https://img-blog.csdnimg.cn/20200227092254684.png)
# 6.2 异常的概念
- **异常**指程序运行过程中出现的非正常现象，例如用户输入错误、除数为零、需要处理的文件不存在、数组下标越界等。
<!--more-->
- 在Java的异常处理机制中，引进了很多用来描述和处理异常的类，称为**异常类**。异常类定义中包含了该类异常的信息和对异常进行处理的方法。
- 所谓**异常处理**，就是指程序在出现问题时依然可以正确的执行完。
- **Java是采用面向对象的方式来处理异常的**。处理过程：
1. **抛出异常**：在执行一个方法时，如果发生异常，则这个方法生成代表该异常的一个对象，停止当前执行路径，并把异常对象提交给JRE。
2. **捕获异常**：JRE得到该异常后，寻找相应的代码来处理该异常。JRE在方法的调用栈中查找，从生成异常的方法开始回溯，直到找到相应的异常处理代码为止。
# 6.3 异常分类
-   Java对异常进行了分类，不同类型的异常分别用不同的Java类表示，所有异常的根类为java.lang.Throwable，Throwable下面又派生了两个子类：Error和Exception。
![classfication](https://img-blog.csdnimg.cn/2020022709314111.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 6.3.1 Error
- **Error**是程序无法处理的错误，表示运行应用程序中较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时 JVM(Java 虚拟机)出现的问题。例如，Java虚拟机运行错误(Virtual MachineError)，当 JVM 不再有继续执行操作所需的内存资源时，将出现 OutOfMemoryError。这些异常发生时，**Java虚拟机(JVM)一般会选择线程终止**。
-  Error 表明系统 JVM 已经处于不可恢复的崩溃状态中。我们不需要管它。
## 6.3.2 Exception
-  **Exception** 是程序本身能够处理的异常，如：
空指针异常(NullPointerException)
数组下标越界异常(ArrayIndexOutOfBoundsException)
类型转换异常(ClassCastException)
算术异常(ArithmeticException)等。

	**Exception 类**是所有异常类的**父类**，其子类对应了各种各样可能出现的异常事件。 通常Java的异常可分为：

1. RuntimeException 运行时异常

2. CheckedException 已检查异常
## 6.3.3 RuntimeException 运行时异常
- **派生于RuntimeException的异常**，如**被 0 除**、**数组下标越界**、**空指针**等，其产生比较频繁，处理麻烦，如果显式的声明或捕获将会对程序可读性和运行效率影响很大。 因此由系统自动检测并将它们交给缺省的异常处理程序(用户可不必对其处理)。
- 这类异常通常是由编程错误导致的，所以在编写程序时，并不要求必须使用异常处理机制来处理这类异常,经常需要通过增加“**逻辑处理来避免这些异常**”。
- **ArithmeticException异常：试图除以0**
![example](https://img-blog.csdnimg.cn/20200227094528930.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **NullPointerException异常**
 解决空指针异常，通常是增加非空判断
![example](https://img-blog.csdnimg.cn/20200227094830290.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **ClassCastException异常**
![example](https://img-blog.csdnimg.cn/2020022709530713.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **ArrayIndexOutOfBoundsException异常**
 解决数组索引越界异常的方式，增加关于边界的判断
![example](https://img-blog.csdnimg.cn/20200227095604146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **NumberFormatException异常**
  数字格式化异常的解决，可以引入正则表达式判断是否为数字
![example](https://img-blog.csdnimg.cn/2020022710010436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 6.3.4 CheckedException 已检查异常
- 所有不是RuntimeException的异常，统称为**Checked Exception**，又被称为“**已检查异常**”，如**IOException**、**SQLException**等以及用户**自定义的Exception异常**。 这类异常在编译时就必须做出处理，否则无法通过编译。
# 6.4 异常的处理方式之一：捕获异常
-  捕获异常是通过3个关键词来实现的：**try-catch-finally**。用try来执行一段程序，如果出现异常，系统抛出一个异常，可以通过它的类型来捕捉(catch)并处理它，最后一步是通过finally语句为异常处理提供一个统一的出口，finally所指定的代码都要被执行(catch语句可有多条;finally语句最多只能有一条，根据自己的需要可有可无)
![note](https://img-blog.csdnimg.cn/2020022710104179.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
1. 即使 try 和 catch 块中存在 return 语句，finally 语句也会执行。是在执行完 finally 语句后再通过 return 退出。

2. finally 语句块只有一种情况是不会执行的，那就是在执行 finally 之前遇到了 System.exit(0) 结束程序运行。
![example](https://img-blog.csdnimg.cn/2020022710251466.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![result](https://img-blog.csdnimg.cn/20200227102538515.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 6.5 异常的处理方式之二：声明异常
- 当CheckedException产生时，不一定立刻处理它，可以再把异常throws出去。
- 在方法中使用try-catch-finally是由这个方法来处理异常。但是在一些情况下，当前方法并不需要处理发生的异常，而是向上传递给调用它的方法处理。
-  如果一个方法中可能产生某种异常，但是并不能确定如何处理这种异常，则应根据异常规范在方法的首部声明该方法可能抛出的异常。
-  如果一个方法抛出多个已检查异常，就必须在方法的首部列出所有的异常，之间以逗号隔开。
![example](https://img-blog.csdnimg.cn/20200227103711139.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![result](https://img-blog.csdnimg.cn/2020022710374377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 6.6 自定义异常
1. 在程序中，可能会遇到JDK提供的任何标准异常类都无法充分描述清楚我们想要表达的问题，这种情况下可以创建自己的异常类，即自定义异常类。

2. 自定义异常类只需从Exception类或者它的子类派生一个子类即可。

3. 自定义异常类如果继承Exception类，则为受检查异常，必须对其进行处理;如果不想处理，可以让自定义异常类继承运行时异常RuntimeException类。

4. 习惯上，自定义异常类应该包含2个构造器：一个是默认的构造器，另一个是带有详细信息的构造器。
![example](https://img-blog.csdnimg.cn/2020022710570388.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)

```java
package io.github.amarisex;

public class TestMyException {
	public static void main(String[] args) {
		Person p = new Person();
		p.setAge(-1);
	}

}

class Person{
	private int age;

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		if(age<0) {
			throw new IllegalAgeException("negative age!");
		}
		this.age = age;
	}
	
}

class IllegalAgeException extends RuntimeException{
	public IllegalAgeException() {	
	}
	
	public IllegalAgeException(String msg) {	
		super(msg);
	}
	
}
```
![result](https://img-blog.csdnimg.cn/20200227105747674.png)
- 使用异常机制的建议

1. 要**避免使用异常处理代替错误处理**，这样会降低程序的清晰性，并且效率低下。
2. 处理异常不可以代替简单测试---只在异常情况下使用异常机制。

3. **不要进行小粒度的异常处理**---应该将整个任务包装在一个try语句块中。

4. 异常往往在**高层处理**

# 6.7 总结
1. Error 与 Exception 都继承自 Throwable 类

2. Error 类层次描述了 Java 运行时系统内部错误和资源耗尽错误。

3. Exception 类是所有异常类的父类，其子类对应了各种各样可能出现的异常事件。

4. 常见的异常类型

      --ArithmeticException

      --NullPointerException

      --ClassCastException

      --ArrayIndexOutOfBoundsException

      --NumberFormatException

5. 方法重写中声明异常原则：子类声明的异常范围不能超过父类声明的范围

6. 异常处理的三种方式

      --捕获异常:try-catch-finally

      --声明异常:throws
7. 自定义异常类只需从Exception类或者它的子类派生一个子类即可。
