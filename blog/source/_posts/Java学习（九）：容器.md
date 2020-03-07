---
title: Java学习（九）：容器
date: 2020-02-27 21:41:51
tags:
	- Java
---
# 9.1 泛型
---
- $Generic$
-  **泛型**是JDK1.5以后增加的，它可以帮助我们建立类型安全的集合。在使用了泛型的集合中，遍历时不必进行强制类型转换。JDK提供了支持泛型的编译器，将运行时的类型检查提前到了编译时执行，提高了代码可读性和安全性。
- **泛**指的数据类**型**
<!--more-->
- 泛型的本质就是“**数据类型的参数化**”。 我们可以把“泛型”理解为数据类型的一个占位符(形式参数)，即告诉编译器，在调用泛型时必须传入实际类型。
- **容器的接口层次结构图**
![容器的接口层次结构图](https://img-blog.csdnimg.cn/20200227161243150.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 9.1.1 自定义泛型
-   我们可以在类的声明处**增加泛型列表**，如：**<T,E,V>**。
此处，字符可以是任何标识符，一般采用这3个字母。

```java
package io.github.amarisex;

public class TestGeneric {
	public static void main(String[] args) {
		myCollection<String> m = new myCollection<>();
		m.set("Amaris", 0);
		m.set("9527", 1);
		
		String a =m.get(1);
		System.out.println(a);
	}

}

class myCollection<E>{
	Object[] objs = new Object[5];
	public void set(E e,int index) {
		objs[index] = e;
	}
	
	@SuppressWarnings("unchecked")
	public E get(int index) {
		return (E) objs[index];
	}
}
```
## 9.1.2 容器中使用泛型
-   容器相关类都定义了泛型，我们在开发和工作中，在使用容器类时都要使用泛型。这样，在容器的存储数据、读取数据时都**避免了大量的类型判断**，非常便捷。
- 泛型类的在集合中的使用![泛型类的在集合中的使用](https://img-blog.csdnimg.cn/20200227163848532.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 9.2 Collection 接口
---
-  **Collection** 表示一组对象，它是集中、收集的意思。Collection接口的两个**子接口是List、Set接口**。
- **Collection接口中定义的方法**
![Collection接口中定义的方法](https://img-blog.csdnimg.cn/20200227200819214.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 9.3 List
---
## 9.3.1 List特点和常用方法
- **List** 是有序、可重复的容器。
1. 有序
List中每个元素都有索引标记。可以根据元素的索引标记(在List中的位置)访问元素，从而精确控制这些元素。
2. 可重复
 List允许加入重复的元素。更确切地讲，List通常允许满足 e1.equals(e2) 的元素重复加入容器。
 -  List接口常用的实现类有3个：ArrayList、LinkedList和Vector。
 - **List 接口中定义的方法**
 ![List 接口中定义的方法](https://img-blog.csdnimg.cn/20200227201432740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![example](https://img-blog.csdnimg.cn/20200227201542897.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 9.3.2 ArrayList特点和底层实现

-  **ArrayList** 底层是用数组实现的存储。
特点：查询效率高，增删效率低，线程不安全。我们一般使用它。
- ArrayList底层使用Object数组来存储元素数据。所有的方法，都围绕这个核心的Object数组来开展。
- ArrayList是可以存放任意数量的对象，长度不受限制，那么它是怎么实现的呢?本质上就是通过定义新的更大的数组，将旧数组中的内容拷贝到新数组，来实现扩容。

## 9.3.3 LinkedList特点和底层实现
-  **LinkedList** 底层用双向链表实现的存储。
特点：查询效率低，增删效率高，线程不安全。
- 双向链表也叫双链表，是链表的一种，它的每个数据节点中都有两个指针，分别指向前一个节点和后一个节点。 所以，从双向链表中的任意一个节点开始，都可以很方便地找到所有节点。
- ![ LinkedList的存储结构图](https://img-blog.csdnimg.cn/20200227203114846.png)
- ![src](https://img-blog.csdnimg.cn/20200227203145547.png)
## 9.3.4 Vector 向量
-  **Vector**底层是**用数组实现的List**，相关的方法都加了同步检查，因此“**线程安全,效率低**”。 比如，indexOf方法就增加了synchronized同步标记。
- 如何选用ArrayList、LinkedList、Vector?

1. 需要线程安全时，用Vector。

2. 不存在线程安全问题时，并且查找较多用ArrayList(一般使用它)。

3. 不存在线程安全问题时，增加或删除元素较多用LinkedList。
# 9.4 Map 接口
---
-  **Map** 就是用来**存储“键(key)-值(value) 对”**的。 Map类中存储的“键值对”通过键来标识，所以“键对象”不能重复。
- Map 接口的实现类有**HashMap**、**TreeMap**、**HashTable**、**Properties**等。
- **Map接口中常用的方法**
![Map接口中常用的方法](https://img-blog.csdnimg.cn/20200227204341135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 9.4.1 HashMap 和 HashTable
-   **HashMap** 采用**哈希算法**实现，是Map接口最常用的实现类。 由于底层采用了哈希表存储数据，我们要求键不能重复，如果发生重复，新的键值对会替换旧的键值对。 HashMap在查找、删除、修改方面都有非常高的效率。
-    HashTable 类和 HashMap 用法几乎一样，底层实现几乎一样，只不过HashTable的方法添加了synchronized关键字确保线程同步检查，效率较低。
- HashMap与HashTable的区别

> 1. HashMap: 线程不安全，效率高。允许key或value为null。
> 2. HashTable: 线程安全，效率低。不允许key或value为null。
```java
package io.github.amarisex;

import java.util.HashMap;
import java.util.Map;

public class TestMap {
	public static void main(String[] args) {
		Map<Integer, String> m1 = new HashMap<>();
		m1.put(1, "Amaris");
		m1.put(2, "97");
		
		System.out.println(m1.get(1));
		System.out.println(m1.size());
		System.out.println(m1.containsKey(2));
		
		Map<Integer, String> m2 = new HashMap<>();
		m2.put(3, "52");
		m1.putAll(m2);
		System.out.println(m1);
	}

}
```
## 9.4.2 HashMap底层实现详解
-  **HashMap** 底层实现采用了**哈希表**，这是一种非常重要的数据结构。对于我们以后理解很多技术都非常有帮助(比如：redis数据库的核心技术和HashMap一样)，因此，非常有必要让大家理解。
数据结构中由数组和链表来实现对数据的存储，他们各有特点。

	> (1) 数组：占用空间连续。 寻址容易，查询速度快。但是，增加和删除效率非常低。
	>(2) 链表：占用空间不连续。 寻址困难，查询速度慢。但是，增加和删除效率非常高。

      那么，我们能不能结合数组和链表的优点(即查询快，增删效率也高)呢? 答案就是“哈希表”。 **哈希表的本质就是“数组+链表”**。
   
# 9.5 Set 接口
---
- **Set接口**继承自**Collection**，Set接口中没有新增方法，方法和Collection保持完全一致。我们在前面通过List学习的方法，在Set中仍然适用。因此，学习Set的使用将没有任何难度。
- Set容器特点：**无序、不可重复**。无序指Set中的元素没有索引，我们**只能遍历查找**;不可重复指**不允许加入重复的元素**。更确切地讲，新元素如果和Set中某个元素通过equals()方法对比为true，则不能加入;甚至，Set中也只能放入一个null元素，不能多个。
-  Set常用的实现类有：**HashSet**、**TreeSet**等，我们一般使用HashSet。
## 9.5.1 HashSet 基本使用
![use](https://img-blog.csdnimg.cn/20200227210432319.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![result](https://img-blog.csdnimg.cn/20200227210445856.png)
## 9.5.2 HashSet 底层实现
-  **HashSet** 是采用**哈希算法**实现，底层**实际是用HashMap实现**的(HashSet本质就是一个**简化版的HashMap**)，因此，**查询效率和增删效率都比较高**。由于 map 中 key 都是不可重复的，因此，Set 天然具有“不可重复”的特性。
## 9.5.3 TreeSet 的使用和底层实现
-  **TreeSet** 底层实际是用 **TreeMap 实现**的，内部维持了一个**简化版的TreeMap**，通过key来存储Set的元素。 TreeSet内部需要对存储的元素进行排序，因此，我们对应的类需要实现Comparable接口。这样，才能根据compareTo()方法比较对象之间的大小，才能进行内部排序。
- 使用TreeSet要点：

	>(1) 由于是二叉树，需要对元素做内部排序。 如果要放入TreeSet中的类  没有实现Comparable接口，则会抛出异常：java.lang.ClassCastException。
	>(2) TreeSet中不能放入null元素。
	
# 9.6 迭代器
- $Itearator$ [ɪtə'reɪtə]
-  如果遇到遍历容器时，判断删除元素的情况，使用迭代器遍历!
- **迭代器遍历List**
```java
package io.github.amarisex;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class TestIterator {
	public static void main(String[] args) {
        List<String> aList = new ArrayList<String>();
        for (int i = 0; i < 5; i++) {
            aList.add("a" + i);
        }
        System.out.println(aList);
        for (Iterator<String> iter = aList.iterator(); iter.hasNext();) {
            String temp = iter.next();
            System.out.print(temp + "\t");
            
        }
        System.out.println();
        System.out.println(aList);
    }

}
```
![result](https://img-blog.csdnimg.cn/20200227212243765.png)
- **迭代器遍历Set**

```java
public class Test {
    public static void main(String[] args) {
        Set<String> set = new HashSet<String>();
        for (int i = 0; i < 5; i++) {
            set.add("a" + i);
        }
        System.out.println(set);
        for (Iterator<String> iter = set.iterator(); iter.hasNext();) {
            String temp = iter.next();
            System.out.print(temp + "\t");
        }
        System.out.println();
        System.out.println(set);
    }
}
```
- **迭代器遍历Map（1）**

```java
public class Test {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<String, String>();
        map.put("A", "高淇");
        map.put("B", "高小七");
        Set<Entry<String, String>> ss = map.entrySet();
        for (Iterator<Entry<String, String>> iterator = ss.iterator(); iterator.hasNext();) {
            Entry<String, String> e = iterator.next();
            System.out.println(e.getKey() + "--" + e.getValue());
        }
    }
}
```
- **迭代器遍历Map（2）**

```java
public class Test {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<String, String>();
        map.put("A", "高淇");
        map.put("B", "高小七");
        Set<String> ss = map.keySet();
        for (Iterator<String> iterator = ss.iterator(); iterator.hasNext();) {
            String key = iterator.next();
            System.out.println(key + "--" + map.get(key));
        }
    }
}
```
# 9.7 遍历集合的方法总结
---
- **遍历List方法一：普通for循环**
![1](https://img-blog.csdnimg.cn/20200227213003645.png)
- **遍历List方法二：增强for循环(使用泛型!)**
![2](https://img-blog.csdnimg.cn/20200227213033100.png)
- **遍历List方法三：使用Iterator迭代器(1)**
![3](https://img-blog.csdnimg.cn/20200227213101431.png)
- **遍历List方法四：使用Iterator迭代器(2)**
![4](https://img-blog.csdnimg.cn/20200227213122786.png)
- **遍历Set方法一：增强for循环**
![5](https://img-blog.csdnimg.cn/20200227213147787.png)
- **遍历Set方法二：使用Iterator迭代器**
![6](https://img-blog.csdnimg.cn/2020022721321158.png)
- **遍历Map方法一：根据key获取value**
![7](https://img-blog.csdnimg.cn/20200227213237403.png)
- **遍历Map方法二：使用entrySet**
![8](https://img-blog.csdnimg.cn/20200227213257897.png)
# 9.8 Collections工具类
---

- 类 **java.util.Collections** 提供了对Set、List、Map进行**排序、填充、查找元素**的辅助方法。
> 1. void sort(List) //对List容器内的元素排序，排序的规则是按照升序进行排序。
	> 2. void shuffle(List) //对List容器内的元素进行随机排列。
	> 3. void reverse(List) //对List容器内的元素进行逆续排列 。
	> 4. void fill(List, Object) //用一个特定的对象重写整个List容器。
	> 5. int binarySearch(List, Object)//对于顺序的List容器，采用折半查找的方法查找特定对象。

- **Collections工具类的常用方法**
![example](https://img-blog.csdnimg.cn/20200227213631476.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
# 9.9 总结
---
1.  Collection 表示一组对象，它是集中、收集的意思，就是把一些数据收集起来。

2. Collection接口的两个子接口：

	a. List中的元素有顺序，可重复。常用的实现类有ArrayList、LinkedList和 vector。

	> Ø ArrayList特点：查询效率高，增删效率低，线程不安全。
	> Ø LinkedList特点：查询效率低，增删效率高，线程不安全。
	>Ø vector特点：线程安全,效率低,其它特征类似于ArrayList。

   	b. Set中的元素没有顺序，不可重复。常用的实现类有HashSet和TreeSet。

	>Ø HashSet特点：采用哈希算法实现,查询效率和增删效率都比较高。
	> Ø TreeSet特点：内部需要对存储的元素进行排序。因此，我们对应的类需要实现Comparable接口。这样，才能根据compareTo()方法比较对象之间的大小，才能进行内部排序。

3. 实现Map接口的类用来存储键(key)-值(value) 对。Map 接口的实现类有HashMap和TreeMap等。Map类中存储的键-值对通过键来标识，所以键值不能重复。

4. Iterator对象称作迭代器，用以方便的实现对容器内元素的遍历操作。

5. 类 java.util.Collections 提供了对Set、List、Map操作的工具方法。

6. 如下情况，可能需要我们重写equals/hashCode方法：

	a. 要将我们自定义的对象放入HashSet中处理。

	b. 要将我们自定义的对象作为HashMap的key处理。

	c. 放入Collection容器中的自定义对象后，可能会调用remove、contains等方法时。

7. JDK1.5以后增加了泛型。泛型的好处：

	a. 向集合添加数据时保证数据安全。

	b. 遍历集合元素时不需要强制转换。
