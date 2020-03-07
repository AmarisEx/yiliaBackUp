---
title:  Java学习（一）：前言
date: 2020-02-18 11:24:35
tags:
	- Java
---

> [Java300课件](https://www.sxt.cn/Java_jQuery_in_action/JVM_JRE_JDK.html)
> [Java教程](https://www.bilibili.com/video/av59814573?from=search&seid=12802959939329126153)

# 应用
软件开发、安卓移动开发、大数据云计算等等领域
# 其他语言
- php（web开发，中小型网站）
- Object_C 和 Swift  (ios开发）
- JavaScript (浏览器ui优化，流行的H5开发核心）
- C# （面向对象，基于Windows桌面软件，旨为抗衡Java，败，缺乏生态）
<!--more-->
- Fortran (复杂计算）
- Basic （easy，消失)
$......$
# 发展史
- James Gosling 创
- 紧随互联网发展
# 核心优势和生态体系
- 核心优势：跨平台
- 紧随互联网发展浪潮，建立强大生态：企业、安卓、大数据、云计算
# 三个版本
- **JavaSE**(Java Standard Edition)：标准版，定位在个人计算机上的应用，发展短板，不如C++
- **JavaEE**(Java Enterprise Edition)：企业版，定位在服务器端的应用
- **JavaME**(Java Micro Edition)：微型版，定位消费性电子产品的应用上（趋于消亡）
# 特性和优势
-  跨平台/可移植性
- 安全性：适合于网络/分布式环境
- 面向对象
- 简单性
- 高性能：通过Java虚拟机优化效率几十倍
- 分布式：为Internet的分布式环境设计
- 多线程：带来更好的交互响应和实时行为
- 健壮性：Java程序不可能造成计算机崩溃，如有异常将其抛出，再通过异常处理机制加以处理
# Java应用程序的运行机制
![Java应用程序的运行机制](https://img-blog.csdnimg.cn/20200217201739136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# JDK、JRE 和 JVM 的作用和区别
- **JVM**(Java Virtual Machine) 是一个虚拟的用于执行bytecode字节码的“虚拟计算机”
- **JRE**(Java Routime Environment) 包含：Java虚拟机、库函数、运行Java应用程序所必须的文件
- **JDK**(Java Development Kit) 包含JRE，以及增加编译器和调试器等用于程序开发的文件
![difference](https://img-blog.csdnimg.cn/20200217202740698.png)
# JDK下载和安装
[下载地址](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
# JDK环境变量PATH设置
- 环境变量是在操作系统中一个具有特定名字的对象，它包含了一个或多个应用程序所将使用到的信息（Path是一个常见的环境变量，它告诉OS，当要求系统运行一个程序而没有告诉它程序所在的完整路径时，系统处理在当前目录下寻找此程序外，还应该到那些目录下寻找
![1](https://img-blog.csdnimg.cn/2020021721050335.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- Path中新增
![2](https://img-blog.csdnimg.cn/20200217210541637.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- 测试
![3](https://img-blog.csdnimg.cn/20200217210559289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# Welcome.java

```java
public class Welcome {
	public static void main(String[] args) {
		System.out.println("Hello,Java world!");
	}
}
```
![cmd_java](https://img-blog.csdnimg.cn/20200217211719651.png)

1. Java对大小写敏感，如果出现了大小写拼写错误，程序无法运行。

2. 关键字public被称作访问修饰符(access modifier)，用于控制程序的其它部分对这段代码的访问级别。

3. 关键字class 的意思是类。Java是面向对象的语言，所有代码必须位于类里面。

4. 一个源文件中至多只能声明一个public的类，其它类的个数不限，如果源文件中包含一个public 类，源文件名必须和其中定义的public的类名相同，且以“.java”为扩展名。

5. 一个源文件可以包含多个类class。

6. 正确编译后的源文件，会得到相应的字节码文件，编译器为每个类生成独立的字节码文件，且将字节码文件自动命名为类的名字且以“.class”为扩展名。

7. main方法是Java应用程序的入口方法，它有固定的书写格式：

8. public static void main(String[]  args) {…} 

9. 在Java中，用花括号划分程序的各个部分，任何方法的代码都必须以“{”开始，以“}”结束， 由于编译器忽略空格，所以花括号风格不受限制。

10. Java中每个语句必须以分号结束，回车不是语句的结束标志，所以一个语句可以跨多行
# 最常用DOS命令
- cd 目录路径：进入一个目录
- cd .. ：进入父目录
- dir ：查看本目录下的文件和子目录列表
- cls : 清空屏幕命令
- 上下键 ：查找敲过的命令
- Tab键 ：自动补齐命令
# 常用开发工具
- **编辑器**：Notepad++, UltraEdit, EditPlus
- **IDE**:[eclipse](https://www.eclipse.org/), Intellij IDE, NetBeans
- [eclipse](https://www.eclipse.org)
![eclipse](https://img-blog.csdnimg.cn/20200217225318845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 桌游小游戏
![desk](https://img-blog.csdnimg.cn/20200218111751235.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![ball](https://img-blog.csdnimg.cn/20200218111804432.png)

```java
package table_tennis;
import java.awt.*;
import javax.swing.*;

public class BallGame extends JFrame{
	
	Image ball = Toolkit.getDefaultToolkit().getImage("images/ball.png");
	Image desk = Toolkit.getDefaultToolkit().getImage("images/desk.jpg");
	
	double x=100;
	double y=100;
	
	double degree = 3.14/3;
	
	//画窗口
	public void paint(Graphics g) {
		//System.out.println("painted");
		g.drawImage(desk, 0, 0, null);
		g.drawImage(ball,(int)x,(int)y,null);
		
		x = x + 10*Math.cos(degree);
		y = y + 10*Math.sin(degree);
		
		//ball_diameter = 30,desk_frame_width = 40,title_frame = 40
		if(y>500-30-40||y<40+40) {
			degree = -degree;
		}
		
		if(x<40||x>856-30-40) {
			degree = 3.14-degree;
		}

	}
	//窗口加载
	void launchFrame() {
		setSize(856,500);
		setLocation(50,50);
		setVisible(true);
		
		//重画
		while(true) {
			repaint();
			try {
				Thread.sleep(40);
			}catch(Exception e) {
				e.printStackTrace();
			}
		}
	}
	public static void main(String[] args) {
		System.out.println("Welcome to BallGame World!");
		BallGame game = new BallGame();
		game.launchFrame();
	}
}
```
# 总结
1. 所有的编程语言的最终目的都是提供一种“抽象”方法。抽象的层次越高，越接近人的思维。越接近人的思维，越容易使用。

2. 越高级的语言越容易学习；当然，这只意味着容易入门；不意味着成为高手越容易，高手仍然需要修炼。

3. Java的核心优势：跨平台。跨平台是靠JVM(虚拟机)实现的。

4. Java各版本的含义：

      JavaSE（Java  Standard  Edition）标准版，定位在个人计算机的应用。

      JavaEE（Java  Enterprise Edition）企业版，定位在服务器端的应用。

      JavaME（Java  Micro  Edition）微型版，定位在消费电子产品的应用。

5. Java程序的开发运行过程为：编写代码、编译、解释运行。

6. JDK用于开发Java程序，JRE是Java运行环境； JVM是JRE的子集，JRE是JDK的子集。

7. JDK配置，需要新建JAVA_HOME环境变量；需要修改Path环境变量。

8. Java是面向对象的语言，所有代码必须位于类里面。main方法是Java应用程序的入口方法。

9. 常见的Java集成开发环境有三个：eclipse、IntelliJ IDE、NetBeans。
