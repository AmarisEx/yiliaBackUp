---
title:  C++：字符串、向量和数组要点小结
date: 2020-03-08 11:29:47
tags:
	- C++
---

# 命名空间的using声明
- `using namespace:name`
-  `using std: cin`

  

  <!--more-->
# string::size_type类型
- 一个无符号类型整数，而且能够存放的下任何`string`对象的大小
- C++中后续的很多地方都有类似的使用, 例如两个迭代器相减得到的距离啊
	```cpp
	string s = "test";
	auto len = s.size();  //此处的len并不是int类型，而是size_type类型
	```
# 基于范围的for语句
- 据说很高效
	```cpp
	string str("some thing");
	for(auto c:str){
	cout<<c<<" ";
	}
	```
# 标准库类型vector
- C++ 中既有类模板也有函数模板，`vector`就是一个类模板
- 初始化
	```cpp
	vector<int> v1(10);  //10个元素，每个都是0
	vector<int> v2{10};  //一个10
	vector<int> v3(10, 1);  //10个1
	vector<int> v4{10, 1};  //10和1
	```
- `psuh_back`
向vector中添加元素： v1.push_back(10);
- 不能以下标形式添加元素
# 迭代器
- 类似于指针，提供了对象的间接访问
- 不同于指针，获取迭代器不是使用取地址符，有迭代器的类型同时拥有返回迭代器的成员，`begin`和`end`
- `end`为尾后迭代器，指向尾元素的下一个位置，根本不存在的，只是个标记而已
- 一般迭代举例
	```cpp
	for(auto it = s.begin();it!=s.end();it++)
	```
	这里明显与不同的是判断条件用来`!=`而不是`<`，这是因为标准库容器都定义了`==`和`!=`, 但是大多都没有`<`以及**下标**
- **某些对vector对象的操作会使迭代器失效**
但凡是使用了迭代器的循环体，都不要向迭代器所属的容器添加元素
# 数组
- 数组的容量是固定的，vector的容量可以动态增长
- 和vector一样，数组的元素应为对象，因此不存在引用的数组
- 不允许拷贝与赋值（☞数组之间的赋值与拷贝）
- **理解复杂的数组声明**
	```cpp
	int *ptrs[10];	//含有10个整型指针的数组
	int &refs[10] = /ag/;	//错误，不存在引用的数组
	int (*Parray)[10] = &arr;	//Parry指向一个含有10个整数的数组，由内而外的理解
	int (&arrRef)[10] = arr;    //arrRef引用一个含有10个整数的数组
	int *(&arry)[10] = ptrs;   //arry是数组的引用，该数组含有10个指针
	```
# C和C++风格字符串
- C: char str[] = {'t', 'e', 's', 't', **'\0'**};  //必须有结束符`'\0'`
- C++: string str = "test";
