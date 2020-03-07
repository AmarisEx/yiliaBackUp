---
title:  LeetCode(2)：两数相加
date: 2020-03-05 11:47:01
tags:
	- LeetCode
	- 数据结构与算法
toc: true
---

# 题干
![题干](https://img-blog.csdnimg.cn/20200305112943384.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
还是太嫩了，写的时候没考虑这些情况（进位之类的），有点被示例误导了
<!--more-->
# 求解
- 时间复杂度：$O(max(m, n))$
- 空间复杂度：$O(max(m, n))$
```java
class Solution {
	public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
		ListNode l3 = new ListNode(0);
		ListNode l = l3;
		ListNode p = l1;
		ListNode q = l2;
		int sum = 0;
		int carry = 0;
		while (p != null || q != null) {
			l3.next = new ListNode(0);
			l3 = l3.next;
			int x = (p != null) ? p.val : 0;
			int y = (q != null) ? q.val : 0;
			sum = x + y + carry;
			carry = sum / 10;
			sum %= 10;
			l3.val = sum;
			if (p != null)
				p = p.next;
			if (q != null)
				q = q.next;
			sum = 0;

		}
		if (carry > 0) {
			l3.next = new ListNode(carry);
		}
		return l.next;

	}
}
```
![result](https://img-blog.csdnimg.cn/20200305113038373.png)
