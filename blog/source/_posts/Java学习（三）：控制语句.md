---
title:  Java学习（三）：控制语句
date: 2020-02-19 12:12:56
tags:
	- Java
---
# 3.1 选择结构
1. **if 单选择结构**

```java
public class Test1 {
    public static void main(String[] args) {
        //通过掷三个骰子看看今天的手气如何？
        int i = (int)(6 * Math.random()) + 1;//通过Math.random()产生随机数
        int j = (int)(6 * Math.random()) + 1;
        int k = (int)(6 * Math.random()) + 1;
        int count = i + j + k;
        //如果三个骰子之和大于15，则手气不错
        if(count > 15) {
            System.out.println("今天手气不错");
        }
    }
}
```
<!--more-->
3.   **if-else 双选择结构**
```java
public class Test {
	public static void main(String[] arg) {
		int r = (int)(6*Math.random());
		if(r<=3) {
			System.out.println("small!");
		}
		else {
			System.out.println("large!");
		}
	}
}
```

  3. if-else if-else多选择结构
    ![if-else if-else多选择结构](https://img-blog.csdnimg.cn/20200219100017409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)


```java
public class Test {
	public static void main(String[] arg) {
		int age = (int)(100*Math.random());
		if(age<18) {
			System.out.println("young");
		}else if(age<60) {
			System.out.println("man");
		}else {
			System.out.println("the aged");
		}
	}
}
```

4.   **switch 结构**
![switch 结构](https://img-blog.csdnimg.cn/20200219100559816.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)

```java
public class Test {
	public static void main(String[] arg) {
		int month = (int)(12*Math.random()) + 1;
		System.out.println("month :" + month);
		switch(month) {
		case 1:
			System.out.println("start");
//			break;
		case 12:
			System.out.println("end");
			break;
		default:
			System.out.println("other");
			break;
		}
	}
}
```
![result](https://img-blog.csdnimg.cn/20200219101458541.png)

- 无 break， 如上述，顺序执行下去
# 3.2 循环结构
- 循环结构分两大类，一类是当型，一类是直到型。
- **当型**
当布尔表达式条件为true时，反复执行某语句，当布尔表达式的值为false时才停止循环，比如：while与for循环。
- **直到型**
先执行某语句， 再判断布尔表达式，如果为true，再执行某语句，如此反复，直到布尔表达式条件为false时才停止循环，比如do-while循环。
## 3.2.1 while 循环

```java
public class Test {
	public static void main(String[] arg) {
		int sum = 0;
		int i=0;
		while(i<=100) {
			sum += i;
			i++;
		}
		System.out.println(sum);
	}
}
```
## 3.2.2 do-while 循环

```java
public class Test {
	public static void main(String[] arg) {
		int sum = 0;
		int i=0;
		do {
			sum += i;
			i++;
		}while(i<=100);
		System.out.println(sum);
	}
}
```
## 3.2.3 for 循环

```java
public class Test {
	public static void main(String[] arg) {
		int sum = 0;
		int i;
		for(i=0;i<=100;i++) {
			sum += i;
		}
		System.out.println(sum);
	}
}
```
## 3.2.4 嵌套循环

```java
public class Test {
	public static void main(String[] arg) {
		int i,j;
		for(j=1;j<=9;j++) {
			for(i=1;i<=j;i++) {
				System.out.print(i+"*"+j+"="+i*j+"\t");
			}
			System.out.println();
		}
	}
}
```
![9*9](https://img-blog.csdnimg.cn/20200219105008458.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 3.2.5 break 语句和 continue 语句
- 在任何循环语句的主体部分，均可用**break**控制循环的流程。break用于**强行退出循环**，不执行循环中剩余的语句。
-  **continue** 语句用在循环语句体中，用于**终止某次循环过程**，即跳过循环体中尚未执行的语句，接着进行下一次是否执行循环的判定。
## 3.2.6 带标签的 break 和 continue
- goto关键字很早就在程序设计语言中出现。尽管goto仍是Java的一个保留字，但并未在Java语言中得到正式使用;Java没有goto语句。然而，在break和continue这两个关键字的身上，我们仍然能看出一些goto的影子---带标签的break和continue。
-  “goto有害”论
- 对Java来说唯一用到标签的地方是在**循环语句之前**。而在循环之前设置标签的唯一理由是：我们希望在其中嵌套另一个循环，由于break和continue关键字通常只中断当前循环，但若随同标签使用，它们就会中断到存在标签的地方。
- **标签必须放在希望跳出的最外层循环之前，并且必须紧跟一个冒号**

```java
public class Test {
	public static void main(String[] arg) {
		int i,j;
		outer:for(i=101;i<=150;i++) {
			for(j=2;j<=i/2;j++) {
				if(i%j==0) {
					continue outer;
				}
			}
				System.out.println(i);
		}
	}
}
```
等价于...
```java
public class Test {
	public static void main(String[] arg) {
		int i,j;
		for(i=101;i<=150;i++) {
			for(j=2;j<=i/2;j++) {
				if(i%j==0) {
					break;
				}
			}
			if(j>i/2) {
				System.out.println(i);
			}
		}
	}
}
```
# 3.3 语句块
- **语句块**(有时叫做复合语句)，是用花括号扩起的任意数量的简单Java语句。
- **块确定了局部变量的作用域**。
- 块中的程序代码，作为一个整体，是要被一起执行的。块可以被嵌套在另一个块中，但是不能在两个嵌套的块内声明同名的变量。**语句块可以使用外部的变量，而外部不能使用语句块中定义的变量**，因为语句块中定义的变量作用域只限于语句块。
![语句块](https://img-blog.csdnimg.cn/2020021911164597.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 3.4 方法
-  **方法**就是一段用来完成特定功能的代码片段，类似于其它语言的**函数**。

```java
public class Test {
	public static void main(String[] arg) {
		System.out.print(add(3,4));
	}
	public static int add(int a, int b) {
		return a+b;
	}
}
```

```java
public class Test {
	public static void main(String[] arg) {
		Test t = new Test();
		int s = t.add(1, 1);
		System.out.print(s);
	}
	int add(int a, int b) {
		return a+b;
	}
}
```
# 3.5 方法的重载（overload）
-   **方法的重载**是指一个类中可以定义多个方法名相同，但参数不同的方法。 调用时，**会根据不同的参数自动匹配对应的方法**。
- 重载的方法，实际是完全不同的方法，只是名称相同而已!
-  构成方法重载的**条件**：
 1. 不同的含义：形参类型、形参个数、形参顺序不同
 2. 只有返回值不同不构成方法的重载
 3.  只有形参的名称不同，不构成方法的重载


# 3.6 递归结构
-   **递归**是一种常见的解决问题的方法，即把问题逐渐简单化。递归的基本思想就是“**自己调用自己**”，一个使用递归技术的方法将会直接或者间接的调用自己。
- **缺陷**
 简单的程序是递归的优点之一。但是递归调用会占用大量的系统堆栈，内存耗用多，在递归调用层次多时速度要比循环慢的多，所以在使用递归时要慎重。
-  任何能用递归解决的问题也能使用迭代解决。
- 递归求阶乘
```java
public class Test {
	public static void main(String[] arg) {
		long t1 = System.currentTimeMillis();
		System.out.printf("%d阶乘的结果:%s%n", 10, factorial(10));
		long t2 = System.currentTimeMillis();
		System.out.printf("递归用时：%s\n",t2-t1);
	}
	static long factorial(int n) {
		if(n==1) {
			return 1;
		}else {
			return n*factorial(n-1);
		}
	}
}
```
![factorial](https://img-blog.csdnimg.cn/20200219120656532.png)

- 循环求阶乘

```java
public class Test {
	public static void main(String[] arg) {
		long t1 = System.currentTimeMillis();
		System.out.printf("阶乘的结果:%s%n", factorialLoop(10));
		long t2 = System.currentTimeMillis();
		System.out.printf("循环用时：%s\n",t2-t1);
	}
	static long factorialLoop(int n) {
		long result = 1;
		while(n>1) {
			result *= n*(n-1);
			n -= 2;
		}
		return result;
	}
}
```
![factorialLoop](https://img-blog.csdnimg.cn/20200219120832690.png)
# 3.7 总结

1. 从结构化程序设计角度出发，程序有三种结构：顺序结构、选择结构和循环结构

2. 选择结构

	（1）if单选择结构 if-else双选择结构 if-else if-else多选择结构

	（2）switch多选择结构

3.  多选择结构与switch的关系：当布尔表达式是等值判断的情况，可使用多重选择结构或switch结构，如果布尔表达式区间判断的情况，则只能使用多重选择结构

	（1） 循环结构
（2） 当型：while与for
	（3） 直到型:do-while

4. while与do-while的区别，在布尔表达式的值为false时while的循环体一次也不执行，而do-while至少执行一次

5. break可以在switch与循环结构中使用，而continue只能在循环结构中使用

6. 方法就是一段用来完成特定功能的代码片段，类似于其它语言的函数

7. 方法的重载是指一个类中可以定义多个方法名相同，但参数不同的方法。 调用时，会根据不同的参数自动匹配对应的方法

8. 任何能用递归解决的问题也能使用迭代解决。在要求高性能的情况下尽量避免使用递归，递归调用既花时间又耗内存。
