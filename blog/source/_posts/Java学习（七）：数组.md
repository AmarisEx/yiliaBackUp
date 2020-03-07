---
title: Java学习（七）：数组
date: 2020-02-21 14:41:47
tags:
	- Java
---
# 7.1 数组概述和特点
- **数组**是相同类型数据的有序集合。
1. 长度是确定的。数组一旦被创建，它的大小就是不可以改变的。

2. 其元素必须是相同类型，不允许出现混合类型。
<!--more-->
3.  数组类型可以是任何数据类型，包括基本类型和引用类型。
-   数组变量属引用类型，数组也可以看成是**对象**，数组中的每个元素相当于该对象的成员变量。数组本身就是对象，Java中对象是在堆中的，因此数组无论保存原始类型还是其他对象类型，数组对象本身是在堆中存储的。
# 7.2 声明与初始化
## 7.2.1 数组的声明
![数组的声明](https://img-blog.csdnimg.cn/20200221101656174.png)
- 声明的时候并没有实例化任何对象，只有在实例化数组对象时，JVM才分配空间，这时才与长度有关。

- 声明一个数组的时候并没有数组真正被创建。

- 构造一个数组，必须指定长度。

## 7.2.2 数组的初始化
- **静态初始化**
  除了用new关键字来产生数组以外，还可以直接在定义数组的同时就为数组元素分配空间并赋值。
  ![静态初始化](https://img-blog.csdnimg.cn/20200221103352100.png)
 - **动态初始化**
数组定义与为数组元素分配空间并赋值的操作分开进行。
 ![动态初始化](https://img-blog.csdnimg.cn/20200221103630721.png)
 - **数组的默认初始化**
    数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。
    ![数组的默认初始化](https://img-blog.csdnimg.cn/20200221103706772.png)
![基本类型数组内存分配图](https://img-blog.csdnimg.cn/20200221102845845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 7.3 遍历_循环_拷贝_java.util.Arrays类
## 7.3.1 数组的遍历
-  数组元素下标的合法区间：[0, length-1]。我们可以通过下标来遍历数组中的元素，遍历时可以读取元素的值或者修改元素的值。
## 7.3.2 for-each 循环
-  **增强for循环for-each**是JDK1.5新增加的功能，专门用于**读取**数组或集合中所有的元素，即对数组进行遍历。
```java
public class Test01 {
	public static void main(String[] args) {
		int[] arr01 = {1,2,3};
		for(int m:arr01) {
			System.out.println(m);
		}
	}
}
```
## 7.3.3 数组的拷贝
![数组的拷贝](https://img-blog.csdnimg.cn/20200221105103779.png)
-    System类里也包含了一个static void arraycopy(object src，int srcpos，object dest， int destpos，int length)方法，该方法可以将src数组里的元素值赋给dest数组的元素，其中srcpos指定从src数组的第几个元素开始赋值，length参数指定将src数组的多少个元素赋给dest数组的元素。

```java
public class Test02 {
	public static void main(String[] args) {
		String[] arr01 = {"UESTC","USTC","MIT"};
		String[] arr02 = new String[4];
		
		System.arraycopy(arr01, 0, arr02, 0, 3);
		
		System.arraycopy(arr01, 2, arr01, 1, 1);//数组的删除元素
		arr01[arr01.length-1] = null;
		
		for(String s:arr02) {
			System.out.println(s);
		}
		
	}
}

```
## 7.3.4 java.util.Arrays 类
-  JDK提供的**java.util.Arrays**类，包含了常用的数组操作，方便我们日常开发。Arrays类包含了：**排序**、**查找**、**填充**、**打印**内容等常见的操作。
- **打印**
![打印数组](https://img-blog.csdnimg.cn/20200221121218521.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
此处的Arrays.toString()方法是Arrays类的静态方法，不是前面讲的Object的toString()方法。
- **排序**
![数组元素的排序](https://img-blog.csdnimg.cn/2020022112123870.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **填充**
![数组的填充](https://img-blog.csdnimg.cn/20200221121321247.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)![fill](https://img-blog.csdnimg.cn/20200221121709750.png)
![fill](https://img-blog.csdnimg.cn/20200221121624429.png)
# 7.4 多维数组
- **多维数组**可以看成以数组为元素的数组。可以有二维、三维、甚至更多维数组，但是实际开发中用的非常少。最多到**二维数组**(学习**容器**后，我们一般使用容器，二维数组用的都很少)。
```java
public class Test02 {
	public static void main(String[] args) {
		int[][] a = new int[3][];
		a[0] = new int[2];
		a[1] = new int[]{1,3};
		a[2] = new int[]{4,5,6};
		
		System.out.println(Arrays.toString(a[2]));
		
		int[][] b = {
				{1,2,3},
				{4,2},
				{7,8,9,0}
		};
		
		System.out.println(Arrays.toString(b[2]));
		
	}
}
```
# 7.5 数组存储表格数据
-   **表格数据模型**是计算机世界最普遍的模型，可以这么说，大家在互联网上看到的所有数据本质上都是“表格”，无非是表格之间互相套用。如下表格是一张雇员表：
![雇员表](https://img-blog.csdnimg.cn/20200221121915817.png)
```java
public class Test02 {
	public static void main(String[] args) {
		Object[] emp1 = {1,"a","01"};
		Object[] emp2 = {2,"b","02"};
		Object[] emp3 = {3,"c","03"};
		
		Object[][] tableData = new Object[3][];
		tableData[0] = emp1;
		tableData[1] = emp2;
		tableData[2] = emp3;
		
		for(Object[] e:tableData) {
			System.out.println(Arrays.toString(e));
		}
	}
}
```
# 7.6 冒泡排序的基础及优化
-  **基础**
```java
package cn.amaris.array01;

import java.util.Arrays;

public class TestBubbleSort {
	public static void main(String[] args) {
		int[] values = {3,1,8,9,4,7,0,2};
		int temp = -1;
		for(int i=0;i<values.length;i++) {
			for(int j=0;j<values.length-1-i;j++) {
				if(values[j]>values[j+1]) {
					temp = values[j];
					values[j] = values[j+1];
					values[j+1] = temp;
				}
			}
			System.out.println(Arrays.toString(values));
		}
	}
}
```
![基础result](https://img-blog.csdnimg.cn/20200221124042266.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **优化**
判断每一趟是否发生了数组元素的交换，如果没有发生，则说明此时数组已经有序，无需再进行后续趟数的比较了。此时可以中止比较。

```java
package cn.amaris.array01;

import java.util.Arrays;

public class TestBubbleSort {
	public static void main(String[] args) {
		int[] values = {3,1,8,9,4,7,0,2};
		int temp = -1;
		boolean flag;
		for(int i=0;i<values.length;i++) {
			flag = true;
			for(int j=0;j<values.length-1-i;j++) {
				if(values[j]>values[j+1]) {
					temp = values[j];
					values[j] = values[j+1];
					values[j+1] = temp;
					
					flag = false;
				}
			}
			System.out.println(Arrays.toString(values));
			if(flag) {
				break;
			}
		}
	}
}
```
![优化result](https://img-blog.csdnimg.cn/20200221124205529.png)
# 7.7 二分法查找
- **二分法检索**(binary search)又称**折半检索**
- 二分法检索的基本思想是设数组中的元素从小到大有序地存放在数组(array)中
首先将给定值key与数组中间位置上元素的关键码(key)比较，如果相等，则检索成功;
否则，若key小，则在数组前半部分中继续进行二分法检索；
 若key大，则在数组后半部分中继续进行二分法检索。
这样，经过一次比较就缩小一半的检索区间，如此进行下去，直到检索成功或检索失败。
  

```java
package cn.amaris.array01;

import java.util.Arrays;

public class TestBinarySearch {
	public static void main(String[] args) {
		int[] arr = { 30, 20, 50, 10, 80, 9, 7, 12, 100, 40, 8 };
		Arrays.sort(arr);

		int value = 10;
		
		System.out.println(myBinarySearch(arr, value));

	}

	public static int myBinarySearch(int[] arr,int value) {
		int low = 0;
		int high = arr.length-1;
		
		while(low<=high) {
			int mid = (low+high)/2;
			
			if(value>arr[mid]) {
				low=mid+1;
			}else if(value<arr[mid]) {
				high=mid-1;
			}else {
				return mid;
			}
		}
		return -1;
	}

}
```
# 7.8 总结
1. 数组是相同类型数据的有序集合。

2. 数组的四个基本特点：

      -- 其长度是确定的

      -- 其元素必须是相同类型

      -- 可以存储基本数据类型和引用数据类型

      -- 数组变量属于引用类型

3. 一维数组的声明方式

      -- type[] arr_name; (推荐使用这种方式)

      -- type arr_name[]。

4. 数组的初始化：静态初始化、动态初始化和默认初始化。

5. 数组的长度:数组名.length，下标的合法区间[0,数组名.length-1]。

6. 数组拷贝:System类中的static void arraycopy(object src，int srcpos，object dest， int destpos，int length)方法。

7. 数组操作的常用类java.util.Arrays类

      -- 打印数组:Arrays.toString(数组名);

      -- 数组排序:Arrays.sort(数组名);

      -- 二分查找:Arrays.binarySearch(数组名,查找的元素)。

8. 二维数组的声明

      -- type[][]arr_name=new type[length][];

      -- type arr_name[][]=new type[length][length]。
