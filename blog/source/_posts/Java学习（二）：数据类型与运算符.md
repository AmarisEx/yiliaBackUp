---
title:  Java学习（二）：数据类型与运算符
date: 2020-02-18 22:07:01
tags:
	- Java
---

# 2.1 注释
- 单行注释：//
- 多行注释：/*...*/，不可嵌套，可行内注释
- 文档注释：/**...*/，注释中包含一些说明性的文字及一些JavaDoc标签（后期写项目时，可以生成项目的API）
<!--more-->
```java
/**
 * @author Amaris
 */
package myfirstproj;

public class TestComment {
	/**
	 * exe 入口
	 * @param args 参数
	 */
	public static void main(String[] args/*test...*/) {
		System.out.println("test comment!");//test...
	}
	/*
	 test...
	*/
}
```
# 2.2 标识符规则
- **标识符**是用来给变量、类、方法以及包进行命名的
- **规则**
    标识符必须以字母、下划线_、美元符号$开头。  

    标识符其它部分可以是字母、下划线“_”、美元符“$”和数字的任意组合。

    Java 标识符大小写敏感，且长度无限制。

    标识符不可以是Java的关键字
    
 - **标识符的使用规范**
   表示类名的标识符，每个单词首字母大写
   表示方法和变量的标识符：第一个单词小写，从第二个单词开始首字母大写即**驼峰原则**，如 eat(), eatFood()
- Java不采用通常语言使用的ASCLL字符集，而是Unicode这样标准的国际字符集
# 2.3 Java 的关键字/保留字
![Java 的关键字保留字](https://img-blog.csdnimg.cn/20200218115943958.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 2.4 变量
## 2.4.1 变量的本质
- **变量的本质上是代表一个“可操作的存储空间**，空间位置是确定的，但是里面放置什么值不确定。我们可通过变量名来访问“对应的存储空间”，从而操纵这个“存储空间”存储的值。

```java
double  salary;
long  earthPopulation;
int  age;
```
![Variable](https://img-blog.csdnimg.cn/20200218120748641.png)

## 2.4.2 变量的分类
- **局部变量**（*local variable*)
方法或语句块内部定义的变量。生命周期是从生命位置开始到方法或语句块执行完毕为止。
- **成员变量**（*member variable*）
也叫实例变量，方法外部、类的内部定义的变量。从属于对象，生命周期伴随对象始终。（对象的成员变量）
![实例变量的默认初始值](https://img-blog.csdnimg.cn/20200218122215207.png)
- **静态变量**（*static variable*）
也叫类变量，使用static定义。从属于类，生命周期伴随类始终，从类加载到卸载。

```java
public class test {
	int a;  //成员变量
	static int b;  //静态变量
	
	public static void main(String[] args) {
		int age;  //局部变量
		age = 18;
		int salary = 21;
	}
}
```
# 2.5 常量(constant)
- **常量**通常指的是一个固定的值，例如：1，2，3，‘a'，true
- Java语言中，主要利用关键字 *final* 来定义一个常量

```java
/*
 * @author zgs
 */
public class test {
	public static void main(String[] args) {
		int age = 21;
		final String NAME = "zgs";
		//name = 'ga';
		final double PI = 3.14;
	}
}
```
- **命名规范** 
所有变量、方法、类名：见名知意

    类成员变量：首字母小写和驼峰原则:  monthSalary

    局部变量：首字母小写和驼峰原则

    常量：大写字母和下划线：MAX_VALUE

    类名：首字母大写和驼峰原则:  Man, GoodMan

    方法名：首字母小写和驼峰原则: run(), runRun()**

# 2.6 基本数据类型(primitive data type)
- **数值型**：byte、short、int、long、float、double
byte127，short 3000，int 21亿
- **字符型**（文本型）：char
- **布尔型**：boolean
  
   ![基本数据类型](https://img-blog.csdnimg.cn/20200218192829962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
   
## 2.6.1 整型变量和常量
-  **整型**用于表示没有小数部分的数值，它允许是负数。整型的范围与运行Java代码的机器无关，这正是Java程序具有很强移植能力的原因之一。与此相反，C和C++程序需要针对不同的处理器选择最有效的整型。
![整型数据类型](https://img-blog.csdnimg.cn/20200218193531890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **Java 语言整型常量的四种表示形式**
**十进制**：...
**八进制**：要求以0开头，如015
**十六进制**：0x或0X
**二进制**：要求以 0b 或 0B 开头，如 0b0100101
- Java 语言的整型常量**默认为int型**，声明 long 型常量可以后加 ‘ l ' 或 ’ L '

```java
		long globalPopulation = 7400000000L;
```
## 2.6.2 浮点型变量和常量
-  带小数的数据在Java中称为**浮点型**。浮点型可分为float类型和double类型。

![浮点型数据类型](https://img-blog.csdnimg.cn/20200218194950384.png)
- **Java 浮点类型常量两种表示形式**
**十进制**：如3.14
**科学计数法**：如314e2，314E2，314E-2
- float类型的数值有一个后缀F或者f ，没有后缀F/f的浮点数值**默认为double类型**。也可以在浮点数值后添加后缀D或者d， 以明确其为double类型。

```java
		float i = 314e-2f;
		double j = 314e2;
```
- **雷区**
不要使用浮点数进行比较！浮点数能够精确表示的数是有限的，因而也是离散的。
 java.math包下面的两个有用的类：BigInteger和BigDecimal，这两个类可以处理任意长度的数值。BigInteger实现了任意精度的整数运算。BigDecimal实现了任意精度的浮点运算。


```java
import java.math.BigDecimal;

/*
 * @author zgs
 */
public class test {
	public static void main(String[] args) {
		BigDecimal bd = BigDecimal.valueOf(1.0);
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        bd = bd.subtract(BigDecimal.valueOf(0.1));
        System.out.println(bd);//0.5
        System.out.println(1.0 - 0.1 - 0.1 - 0.1 - 0.1 - 0.1);//0.5000000000000001
        
        BigDecimal bd2 = BigDecimal.valueOf(0.1);
        BigDecimal bd3 = BigDecimal.valueOf(1/10);
        System.out.println(bd2 == bd3);
        System.out.println(bd2.equals(bd3));
	}
} 
```
![result](https://img-blog.csdnimg.cn/20200218201303893.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 2.6.3 字符型变量和常量
-   字符型在内存中占2个字节，在Java中使用单引号来表示字符常量。
-    Unicode具有从0到65535之间的编码，他们通常用从’\u0000’到’\uFFFF’之间的十六进制值来表示（前缀为u表示Unicode） 

```java
		char a = 65;
		char b = '\u0041';
		char c = 'A';
```
- **转义字符**
![转义字符](https://img-blog.csdnimg.cn/20200218202311897.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 2.6.4 boolean 类型变量和常量
-   boolean类型有两个常量值，true和false，在内存中占一位（不是一个字节），**不可以使用 0 或非 0 的整数替代 true 和 false** ，这点和C语言不同。 boolean 类型用来判断逻辑条件，一般用于程序流程控制 。
- $Less\ is\ More$
# 2.7 运算符(operator)
![operator](https://img-blog.csdnimg.cn/20200218203130763.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 2.7.1 算术运算符
- **整数运算**
1. 如果两个操作数有一个为Long, 则结果也为long。

2. 没有long时，结果为int。即使操作数全为short，byte，结果也是int。

- **浮点运算**

1. 如果两个操作数有一个为double，则结果为double。
2. 只有两个操作数都是float，则结果才为float。
3. 整数和浮点运算时，优先为浮点
- **取模运算**
.其操作数可以为浮点数,一般使用整数，结果是“余数”，“余数”符号和左边操作数相同，如：7%3=1，-7%3=-1，7%-3=1。
- **一元运算符**
算术运算符中++，--属于一元运算符，该类运算符只需要一个操作数。
## 2.7.2 赋值及其扩展赋值运算符
![赋值及其扩展赋值运算符](https://img-blog.csdnimg.cn/20200218204710560.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 2.7.3 关系运算符
![关系运算符](https://img-blog.csdnimg.cn/20200218205112927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
-  =是赋值运算符，而真正的判断两个操作数是否相等的运算符是==。

-  ==、!= 是所有（基本和引用）数据类型都可以使用

- \>、>=、 <、 <= 仅针对数值类型（byte/short/int/long,  float/double。以及char）
## 2.7.4 逻辑运算符
![逻辑运算符](https://img-blog.csdnimg.cn/2020021820592830.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)

-  短路与和短路或采用短路的方式。从左到右计算，如果只通过运算符左边的操作数就能够确定该逻辑表达式的值，则不会继续计算运算符右边的操作数，**提高效率**。

```java
		boolean b = 1>2&&2<(3/0);
```
## 2.7.5 位运算符
![位运算符](https://img-blog.csdnimg.cn/20200218211255390.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 2.7.6 字符串连接符
- “+”运算符两侧的操作数中只要有一个是字符串(String)类型，系统会自动将另一个操作数转换为字符串然后再进行连接。
## 2.7.7 条件运算符

```java
x ? y : z
```
-  其中 x 为 boolean 类型表达式，先计算 x 的值，若为true，则整个运算的结果为表达式 y 的值，否则整个运算结果为表达式 z 的值。


## 2.7.8 运算符优先级
![运算符优先级](https://img-blog.csdnimg.cn/20200218213238173.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 2.8 类型转换
## 2.8.1 自动类型转换
-    **自动类型转换**指的是容量小的数据类型可以自动转换为容量大的数据类型。如图2-6所示，黑色的实线表示无数据丢失的自动类型转换，而虚线表示在转换时可能会有精度的损失。
![自动类型转换](https://img-blog.csdnimg.cn/20200218213913499.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
-  可以将整型常量直接赋值给byte、 short、 char等类型变量，而不需要进行强制类型转换，只要不超出其表数范围即可。（$ASCLL$)
## 2.8.2 强制类型转换
- **强制类型转换**，又被称为造型，用于显式的转换一个数值的类型。在有可能丢失信息的情况下进行的转换是通过造型来完成的，但可能造成精度降低或溢出。
- (type)var
## 2.8.3 类型转换时常见错误问题

- **超范围**
```java
int money = 1000000000; //10亿
int years = 20;
//返回的total是负数，超过了int的范围
int total = money*years;
System.out.println("total="+total);
//返回的total仍然是负数。默认是int，因此结果会转成int值，再转成long。但是已经发生//了数据丢失
long total1 = money*years; 
System.out.println("total1="+total1);
//返回的total2正确:先将一个因子变成long，整个表达式发生提升。全部用long来计算。
long total2 = money*((long)years); 
System.out.println("total2="+total2);
```
- **l与1混淆**
long类型使用大写L不要用小写。
# 简单的键盘输入和输出

```java
import java.util.Scanner;

/*
 * @author zgs
 */
public class test {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Please input your name: ");
		String name = scanner.nextLine();
		System.out.println("Hello, " + name + " !");
	}
}
```
![简单的键盘输入和输出](https://img-blog.csdnimg.cn/20200218220045869.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 2.9 总结
1. 注释可以提高程序的可读性。可划分为

2. 单行注释  //

3. 多行注释  /*...*/

4. 文档注释  /**...*/

5. 标识符的命名规则：

6. 标识符必须以字母、下划线_、美元符号$开头。  

7. 标识符其它部分可以是字母、下划线“_”、美元符“$”和数字的任意组合。

8. Java 标识符大小写敏感，且长度无限制。

9. 标识符不可以是Java的关键字。

10. 标识符的命名规范

11. 表示类名的标识符：每个单词的首字母大写，如Man, GoodMan

12. 表示方法和变量的标识符：第一个单词小写，从第二个单词开始首字母大写，我们称之为“驼峰原则”，如eat(), eatFood()

13. 变量的声明格式：

	type  varName  [=value] [,varName[=value]...];

14. 变量的分类：局部变量、实例变量、静态变量

15. 常量的声名格式

	final  type  varName = value ;

16. Java的数据类型可分为基本数据类型和引用数据类，基本数据类型的分类如下：

17. 整型变量：byte、short、int、long

18. 浮点型：float、double

19. 字符型：char

20. 布尔型:boolean，值为true或者false

21. Java语言支持的运算符可分为：

22. 算术运算符:  +，-，*，/，%，++，--

23. 赋值运算符 = 

24. 扩展赋值运算符:+=，-=，*=，/= 

25. 关系运算符:  >，<，>=，<=，==，!= ，instanceof

26. 逻辑运算符:  &&，||，!

27. 位运算符:  &，|，^，~ ， >>，<<，>>> 

28. 字符串连接符：+

29. 条件运算符 ？： 

30. 基本数据类型的类型转换可分为：

31. 自动类型转换：容量小的数据类型可以自动转换为容量大的数据类型

32. 强制类型转换：用于显式的转换一个数值的类型，语法格式：(type)var

33. 键盘的输入：Scanner类的使用
