---
title:  LeetCode(3)：无重复字符的最长子串
date: 2020-03-06 10:22:59
tags:
	- LeetCode
	- 数据结构与算法
toc: true
---

# 题干
![ex](https://img-blog.csdnimg.cn/20200306101028882.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
<!--more-->
# 求解
- 根据题干的描述，要确定最长无重复字符字串的长度，我们可以使用一个队列；
依次向队列中加入字符，若不存在在入队，反之，出队（直至去除重复字符）
```c
class Solution {
	public int lengthOfLongestSubstring(String s) {
		if(s.trim().isEmpty()&&(!s.isEmpty()))return 1;
		if(s.isEmpty())return 0;
		Queue<Character> q = new LinkedList<Character>();
		int maxLength=1,length=1;
		q.add(s.charAt(0));
		
		for(int i=1;i<s.length();i++) {
			if(q.contains(s.charAt(i))) {
				while(!q.element().equals(s.charAt(i))) {
					q.remove();
					length--;
				}
				q.remove();
				length--;
			}
			q.add(s.charAt(i));
			length++;
			if(length>maxLength) {
				maxLength=length;
			}
		}
		
		return maxLength;
		
	}
}
```
![result](https://img-blog.csdnimg.cn/20200306101649528.png)
# 官方题解
- 遍历给定字符串 s 的所有可能的子字符串并调用函数 allUnique。 如果事实证明返回值为 true，那么我们将会更新无重复字符子串的最大长度的答案。
```c
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int ans = 0;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j <= n; j++)
                if (allUnique(s, i, j)) ans = Math.max(ans, j - i);
        return ans;
    }

    public boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i < end; i++) {
            Character ch = s.charAt(i);
            if (set.contains(ch)) return false;
            set.add(ch);
        }
        return true;
    }
}

```

