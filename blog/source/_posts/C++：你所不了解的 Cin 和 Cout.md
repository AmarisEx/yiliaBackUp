---
title:  C++：你所不了解的 Cin 和 Cout
date: 2020-03-03 22:02:08
tags:
	- C++
toc: true
---


# 基本概念
- Cin 和 Cout  从属于iostream标准库
-  cin 是 istream 类型的**对象**(划重点），用作基本输入
-  cout 是 ostream 类型的**对象**(划重点），用作基本输出

<!--more-->

# 使用详解

```cpp
# include<iostream>
using namespace std;

int main()
{
	int i = 0, j = 0;
	cin >> i >> j;
	cout << "The sum of " << i << " and " << j
		<< " is " << i + j << endl;


	return 0;
}
```
## 输入运算符
- 在上述求两数之和的程序中，用户先输入变量$i$和$j$的值，此过程中，**输入运算符 >>** 接受一个 **istream** 对象作为其左侧运算对象，接受一个对象作为其右侧运算对象。它从给定的 istream 中读入数据，并存入给定对象中。
- 输入运算符**返回其左侧**运算对象作为其计算结果，因此，此表达式等价于

	```cpp
	(cin >> i) >> j;
	```
	即：
	
	```cpp
	cin >> i;
	cin >> j;
	```
## 输出运算符
- 与输入运算符类似，**输出运算符 <<** 左侧必须是 **ostream** 类型的对象，右侧的运算对象是需要打印的值
- 输出运算符也**返回其左侧**运算对象作为其计算结果
# 简单应用：读入数量不定的输入数据

```cpp
# include<iostream>
using namespace std;

int main()
{
	int sum = 0, value = 0;
	while (cin >> value) {
		sum += value;
	}
	cout << "Sum is: " << sum << endl;

	return 0;
}
```
- 重点是 while 语句的条件：**while (cin >> value)**
当我们使用一个 istream 对象作为条件时，其效果是检测流的状态。如果流是有效的，即流未遇到错误，那么检测成功。当遇到文件结束符（windows中使用ctrl+z)，或遇到一个无效输入时（例如输入类型错误），istream 对象的状态会变为无效。处于无效的 istream 对象会使条件变为假。
