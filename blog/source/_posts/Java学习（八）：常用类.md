---
title: Java学习（八）：常用类
date: 2020-02-26 22:21:27
tags:
	- Java
---
# 8.1 包装类
-  Java是面向对象的语言，但并不是“纯面向对象”的，因为我们经常用到的基本数据类型就不是对象。但是我们在实际应用中经常需要将基本数据转化成对象，以便于操作。比如：将基本数据类型存储到Object[]数组或集合中的操作等等。
- 为了解决这个不足，Java在设计类时为每个基本数据类型设计了一个对应的类进行代表，这样八个和基本数据类型对应的类统称为**包装类(Wrapper Class)**。
<!--more-->
## 8.1.1 包装类基本知识
- 包装类均位于java.lang包
- 八种包装类和基本数据类型的对应关系
![八种包装类和基本数据类型的对应关系](https://img-blog.csdnimg.cn/2020022309412269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
    在这八个类名中，除了Integer和Character类以外，其它六个类的类名和基本数据类型一致，只是类名的第一个字母大写而已。
  
## 8.1.2 包装类的用途
1.  作为和基本数据类型对应的类型存在，方便涉及到对象的操作，如Object[]、集合等的操作。

2. 包含每种基本数据类型的相关属性如最大值、最小值等，以及相关的操作方法(这些操作方法的作用是在基本数据类型、包装类对象、字符串之间提供相互之间的转化!)。

```java
package io.github.amarisex;

public class TestWrappedClass {
	public static void main(String[] args) {
		// 基本数据类型转成包装类对象
		Integer a = new Integer(3);
		System.out.println(a);
		Integer b = Integer.valueOf(4);// ***

		// 把包装类对象装成基本数据类型
		int c = b.intValue();
		
		// 把字符串转成包装类对象
		Integer e = new Integer("123");
		System.out.println(e);
		
		// 把包装类对象转成字符串
		String str = e.toString();
		System.out.println(str);
	}
}
```
## 8.1.3 自动装箱和拆箱
-    **自动装箱和拆箱**就是将基本数据类型和包装类之间进行自动的互相转换。JDK1.5后，Java引入了自动装箱(autoboxing)/拆箱(unboxing)。
- **自动装箱**
基本类型的数据处于需要对象的环境中时，会自动转为“对象”。
我们以Integer为例：在JDK1.5以前，这样的代码 Integer i = 5 是错误的，必须要通过Integer i = new Integer(5) 这样的语句来实现基本数据类型转换成包装类的过程;而在JDK1.5以后，Java提供了自动装箱的功能，因此只需**Integer i = 5**这样的语句就能实现基本数据类型转换成包装类，这是因为JVM为我们执行了Integer i = Integer.valueOf(5)这样的操作，这就是Java的自动装箱。
![自动装箱](https://img-blog.csdnimg.cn/20200225094106565.png)
- **自动拆箱**
每当需要一个值时，对象会自动转成基本数据类型，没必要再去显式调用intValue()、doubleValue()等转型方法。
如 **Integer i = 5;int j = i;** 这样的过程就是自动拆箱。
![自动拆箱](https://img-blog.csdnimg.cn/20200225094131248.png)
-  **自动装箱**过程是通过调用包装类的**valueOf()方法**实现的，而**自动拆箱**过程是通过调用包装类的 **xxxValue()方法**实现的(xxx代表对应的基本数据类型，如intValue()、doubleValue()等)。
- **包装类空指针异常问题**
![包装类空指针异常问题](https://img-blog.csdnimg.cn/20200225094448241.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
-   null表示i没有指向任何对象的实体，但作为对象名称是合法的(不管这个对象名称存是否指向了某个对象的实体)。由于实际上i并没有指向任何对象的实体，所以也就不可能操作intValue()方法，这样上面的写法在运行时就会出现NullPointerException错误。
## 8.1.4 包装类的缓存问题
- 整型、char类型所对应的包装类，在自动装箱时，对于**-128~127**之间的值会进行缓存处理，其目的是提高效率。
-  缓存处理的原理为：如果数据在-128~127这个区间，那么在类加载时就已经为该区间的每个数值创建了对象，并将这256个对象存放到一个名为cache的数组中。每当自动装箱过程发生时(或者手动调用valueOf()时)，就会先判断数据是否在该区间，如果**在**则**直接获取**数组中对应的包装类对象的引用，如果**不在该区间**，则会通过**new**调用包装类的构造方法来创建对象。
-  包装类在自动装箱时为了提高效率，对于-128~127之间的值会进行缓存处理。**超过范围**后，对象之间**不能再使用==进行数值的比较**，而是使用equals方法。

```java
package io.github.amarisex;

public class TestWrappedClass {
	public static void main(String[] args) {
		Integer i1 = 1234;
		Integer i2 = 1234;
		Integer i3 = 123;
		Integer i4 = 123;
		System.out.println(i1==i2);
		System.out.println(i1.equals(i2));
		System.out.println(i3==i4);
		System.out.println(i3.equals(i4));
	}
}
```
![result](https://img-blog.csdnimg.cn/20200225192032314.png)
# 8.2 String 类
## 8.2.1 String 类
-   **String 类**对象代表**不可变的Unicode字符序列**，因此我们可以将String对象称为“不可变对象”。 那什么叫做“不可变对象”呢?指的是对象内部的成员变量的值无法再改变（**final**)
![src](https://img-blog.csdnimg.cn/2020022519232386.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 8.2.2 StringBuild 和 StringBuffer
-   StringBuffer和StringBuilder非常类似，均代表可变的字符序列。 这两个类都是抽象类AbstractStringBuilder的子类，方法几乎一模一样。
1. StringBuffer JDK1.0版本提供的类，线程安全，做线程同步检查， 效率较低。
2. StringBuilder JDK1.5版本提供的类，线程不安全，不做线程同步检查，因此效率较高。 建议采用该类。
- 常用方法列表：

3. 重载的public StringBuilder append(…)方法
4. 可以为该StringBuilder 对象添加字符序列，仍然返回自身对象。
5. 方法 public StringBuilder delete(int start,int end)
可以删除从start开始到end-1为止的一段字符序列，仍然返回自身对象。
6. 方法 public StringBuilder deleteCharAt(int index)移除此序列指定位置上的 char，仍然返回自身对象。
7. 重载的public StringBuilder insert(…)方法
可以为该StringBuilder 对象在指定位置插入字符序列，仍然返回自身对象。
8. 方法 public StringBuilder reverse()
用于将字符序列逆序，仍然返回自身对象。
9. 方法 public String toString() 返回此序列中数据的字符串表示形式。
10. 和 String 类含义类似的方法：
![example](https://img-blog.csdnimg.cn/20200225194121610.png)

```java
package io.github.amarisex;

public class TestWrappedClass {
	public static void main(String[] args) {
		StringBuilder s1 = new StringBuilder("Amaris");
		s1.append('E');
		s1.append('x');
		System.out.println(s1);
		System.out.println(s1.reverse().reverse());
		System.out.println(s1.delete(6,8));
		System.out.println(s1.insert(6, "Ex"));
	}
}
```
![result](https://img-blog.csdnimg.cn/20200225194525293.png)
# 8.3 时间处理相关类
- 在计算机世界，我们把1970 年 1 月 1 日 00:00:00定为基准时间，每个度量单位是毫秒(1秒的千分之一)
![时间处理相关类](https://img-blog.csdnimg.cn/20200225195428180.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 8.3.1 Date 时间类(java.util.Date)
-   在标准Java类库中包含一个Date类。它的对象表示一个特定的瞬间，精确到毫秒。
1. Date() 分配一个Date对象，并初始化此对象为系统当前的日期和时间，可以精确到毫秒)。

2. Date(long date) 分配 Date 对象并初始化此对象，以表示自从标准基准时间(称为“历元(epoch)”，即 1970 年 1 月 1 日 00:00:00 GMT)以来的指定毫秒数。

3. boolean after(Date when) 测试此日期是否在指定日期之后。

4. booleanbefore(Date when) 测试此日期是否在指定日期之前。

5. boolean equals(Object obj) 比较两个日期的相等性。
6.  long getTime() 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。

7. String toString() 把此 Date 对象转换为以下形式的 String：
dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun、 Mon、Tue、Wed、 Thu、 Fri、 Sat)。

```java
package io.github.amarisex;
import java.util.Date;

public class TestData {
	public static void main(String[] args) {
		Date d1 = new Date();
		Date d2 = new Date(d1.getTime()+1000);
		System.out.println(d1.equals(d2));

	}
}
```
## 8.3.2 DateFormat类和SimpleDateFormat类·DateFormat类的作用
- 把时间对象转化成指定格式的字符串。反之，把指定格式的字符串转化成时间对象。
DateFormat是一个抽象类，一般使用它的的子类**SimpleDateFormat**类来实现。
- DateFormat类的作用
  把时间对象转化成指定格式的字符串。反之，把指定格式的字符串转化成时间对象。
DateFormat是一个抽象类，一般使用它的的子类SimpleDateFormat类来实现。

```java
package io.github.amarisex;

import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;

public class TestDateFormat {
	public static void main(String[] args) {
		DateFormat df = new SimpleDateFormat("yyyy-MM-dd:hh:mm:ss-a");
		
		String s1 = df.format(new Date());
		System.out.println(s1);
	}

}
```
![result](https://img-blog.csdnimg.cn/20200225202544487.png)
![格式化字符的含义](https://img-blog.csdnimg.cn/20200225201839224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 8.3.3 Calendar 日历类
- Calendar 类是一个抽象类，为我们提供了关于日期计算的相关功能，比如：年、月、日、时、分、秒的展示和计算。
 **GregorianCalendar** 是 Calendar 的一个具体子类，提供了世界上大多数国家/地区使用的标准日历系统。


```java
package io.github.amarisex;

import java.util.Calendar;
import java.util.GregorianCalendar;
import java.util.Date;

public class TestCalendar {
	public static void main(String[] args) {
		GregorianCalendar c1 = new GregorianCalendar(2020,3,1,8,0,0);
		System.out.println(c1.get(Calendar.YEAR));
		System.out.println(c1.get(Calendar.DATE));
		System.out.println(c1.get(Calendar.DAY_OF_WEEK));
		
		//设置日期
		Calendar c2 = new GregorianCalendar();
		Calendar c3 = new GregorianCalendar();
		System.out.println(c2);
		 // 日期计算
		c3.add(Calendar.YEAR, -100);
		c2.set(Calendar.YEAR, 2021);
		System.out.println(c2.get(Calendar.DAY_OF_WEEK));
		 // 日历对象和时间对象转化
		Date d1 = c3.getTime();
		System.out.println(d1);
		printCalendar(c2);
	}
	
	public static void printCalendar(Calendar c) {
		int year = c.get(Calendar.YEAR);
	    int month = c.get(Calendar.MONTH) + 1;
	    int day = c.get(Calendar.DAY_OF_MONTH);
	    int date = c.get(Calendar.DAY_OF_WEEK) - 1; // 星期几
	    String week = "" + ((date == 0) ? "日" : date);
	    int hour = c.get(Calendar.HOUR);
	    int minute = c.get(Calendar.MINUTE);
	    int second = c.get(Calendar.SECOND);
	    System.out.printf("%d年%d月%d日,星期%s %d:%d:%d\n", year, month, day,  
	                    week, hour, minute, second);
		
	}

}
```
![result](https://img-blog.csdnimg.cn/20200225210213799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)

```java
package io.github.amarisex;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.GregorianCalendar;
import java.util.Scanner;
import java.util.Date;

public class TestCalendar {
	public static void main(String[] args) throws ParseException {
		//String str = "2020-10-10";
		Scanner scanner = new Scanner(System.in);
		System.out.println("Please input the date as like 2000-9-16: ");
		String str = scanner.nextLine();
		DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
		Date date = df.parse(str);
		Calendar c = new GregorianCalendar();
		c.setTime(date);

		System.out.println("日\t一\t二\t三\t四\t五\t六");
		int day = c.get(Calendar.DAY_OF_MONTH);
		c.set(Calendar.DAY_OF_MONTH, 1);
		
		for(int i=0;i<c.get(Calendar.DAY_OF_WEEK)-1;i++) {
			System.out.print("\t");
		}
		
		int maxMonth = c.getActualMaximum(Calendar.DATE);
		for (int i = 1; i < maxMonth; i++) {
			System.out.print(c.get(Calendar.DAY_OF_MONTH)+"");
			if(i!=day) {
				System.out.print("\t");
			}else {
				System.out.print("*\t");
			}
			if(c.get(Calendar.DAY_OF_WEEK)==7) {
				System.out.println();
			}
			c.add(Calendar.DAY_OF_MONTH, 1);

		}

	}

}
```
![result](https://img-blog.csdnimg.cn/2020022619262046.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 8.4 Math 类
- java.lang.Math提供了一系列静态方法用于科学计算;其方法的参数和返回值类型一般为double型。如果需要更加强大的数学运算能力，计算高等数学中的相关内容，可以使用apache commons下面的Math类库。
- Math类的常用方法：

1. abs 绝对值

2. acos,asin,atan,cos,sin,tan 三角函数

3.  sqrt 平方根

4.  pow(double a, double b) a的b次幂

5.  max(double a, double b) 取大值
6. min(double a, double b) 取小值

7. ceil(double a) 大于a的最小整数

8. floor(double a) 小于a的最大整数

9. random() 返回 0.0 到 1.0 的随机数

 10. long round(double a) double型的数据a转换为long型(四舍五入)

11. toDegrees(double angrad) 弧度->角度

 12. toRadians(double angdeg) 角度->弧度

# 8.5 File 类
## 8.5.1 File类的基本用法
-    **java.io.File类**：代表文件和目录。 在开发中，读取文件、生成文件、删除文件、修改文件的属性时经常会用到本类。

-   以pathname为路径创建File对象，如果pathname是相对路径，则默认的当前路径在系统属性user.dir中存储
```java
package io.github.amarisex;

import java.io.File;
import java.io.IOException;

public class TestFile {
	public static void main(String[] args) throws IOException {
		File f = new File("c:/users/18655/desktop/test.txt");
		f.createNewFile();
		System.out.println(f);
		f.renameTo(new File("c:/users/18655/desktop/test.txt"));
		
	}

}
```
- 测试File类访问属性的基本用法
![测试File类访问属性的基本用法](https://img-blog.csdnimg.cn/20200226195029192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)- 使用mkdir创建目录

```java
package io.github.amarisex;

import java.io.File;
import java.io.IOException;
import java.util.Date;

public class TestFile {
	public static void main(String[] args) throws IOException {
		File f = new File("c:/users/18655/desktop/test.txt");
        f.createNewFile(); // 会在desktop下面生成c.txt文件
        f.delete(); // 将该文件或目录从硬盘上删除
        File f2 = new File("c:/users/18655/desktop/testFile");
        boolean flag = f2.mkdir(); //目录结构中有一个不存在，则不会创建整个目录树
        System.out.println(flag);//创建失败
		
	}

}
```
- 使用mkdirs创建目录
![result](https://img-blog.csdnimg.cn/20200226195526196.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 8.5.2 递归遍历目录结构和树状展现

```java
package io.github.amarisex;

import java.io.File;
import java.io.IOException;

public class TestFile {
	public static void main(String[] args) throws IOException {
		File f = new File("C:\\Users\\18655\\Desktop\\常驻文件夹\\项目一总报告\\最小网元设计总报告\\附件");
		printFile(f,0);
	}
	
	static void printFile(File f,int level) {
		for(int i=0;i<level;i++) {
			System.out.print("- ");
		}
		System.out.println(f.getName());
		if(f.isDirectory()) {
			File[] files = f.listFiles();
			
			for(File temp:files) {
				printFile(temp,level+1);
			}
		}
	}

}
```
![result](https://img-blog.csdnimg.cn/20200226200929918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 8.6 枚举
-   JDK1.5引入了枚举类型。枚举类型的定义包括枚举声明和枚举体
-    所有的枚举类型隐性地继承自 java.lang.Enum。枚举实质上还是类!而每个被枚举的成员实质就是一个枚举类型的实例，他们默认都是**public static final**修饰的。可以直接通过枚举类型名使用它们。
![example](https://img-blog.csdnimg.cn/20200226201248161.png)
1. 当你需要定义一组常量时，可以使用枚举类型。

2. 尽量不要使用枚举的高级特性，事实上高级特性都可以使用普通类来实现，没有必要引入枚举，增加程序的复杂性!

```java
package io.github.amarisex;

public class TestFile {
	public static void main(String[] args){
		Season s = Season.Autumn;
		switch(s) {
		case Spring:
	        System.out.println("春天");
	        break;
	    case Summer:
	        System.out.println("夏天");
	        break;
	    case Autumn:
	        System.out.println("秋天");
	        break;
	    case Winter:
	        System.out.println("冬天");
	        break;
	    }
	}
	
}
enum Season{
	Spring,Summer,Autumn,Winter
};
```
# 8.7 总结
1. 每一个基本数据类型对应一个包装类。

2. 包装类的用途：

      作为和基本数据类型对应的引用类型存在，方便涉及到对象的操作。

      包含每种基本数据类型的相关属性如最大值、最小值以及相关的操作方法。

3. JDK1.5后在Java中引入自动装箱和拆箱。

4. 字符串相关类String、StringBuffer与StringBuilder

      String：不可变字符序列。

      StringBuffer：可变字符序列，并且线程安全，但是效率低。

      StringBuilder：可变字符序列，线程不安全，但是效率高(一般用它)。

      日期与时间类Date、DateFormat、SimpleDateFormat、Calendar、GregorianCalendar。

5. Math类的常用方法

      pow(double a,double b)

      max(double a,double b)

      min(double a,double b)

      random()

      long round(double a)

6. 与操作文件相关的File类。

7. 当需要定义一组常量时，使用枚举类型。
