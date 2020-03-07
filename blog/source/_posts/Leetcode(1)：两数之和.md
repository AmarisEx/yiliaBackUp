---
title:  Leetcode(1)：两数之和
date: 2020-03-05 10:18:49
tags:
	- LeetCode
	- 数据结构与算法
toc: true
---

# 法一：暴力求解
- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$
<!--more-->

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i,j;
        int[] result = new int[2];
        for(i=0;i<nums.length-1;i++){
            for(j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                    result[0] = i;
                    result[1] = j;
                    return result;
                }
            }
        }
        return result;
    }
}
```
![result](https://img-blog.csdnimg.cn/20200223091845942.png)菜到晕厥...
# 法二：两遍哈希表
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$
- 以空间换取速度
```java
class Solution {
	public int[] twoSum(int[] nums, int target) {
		Map<Integer, Integer> map = new HashMap<>();
		for (int i = 0; i < nums.length; i++) {
			map.put(nums[i], i);
		}
		for (int i = 0; i < nums.length; i++) {
			int complement = target - nums[i];
			if (map.containsKey(complement) && map.get(complement) != i) {
				return new int[] { i, map.get(complement) };
			}
		}
		throw new IllegalArgumentException("No two sum solution");
	}
}
```
![result](https://img-blog.csdnimg.cn/20200305094602507.png)
- 初看这段代码，你可能会以为在哈希表中查找元素不也是$O(n)$吗，这恰恰是问题的关键。哈希表采用的是**映射**的关系（映射函数），这使得在**没有冲突**的情况下，，时间复杂度就是$O(1)$。
# 法三：一遍哈希表
- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> map  = new HashMap<>();
        for(int i=0;i<nums.length;i++) {
        	int complement = target-nums[i];
        	if(map.containsKey(complement)&&map.get(complement)!=i) {
        		return new int[] {i,map.get(complement)};
        	}
        	map.put(nums[i], i);
        }
        throw new IllegalArgumentException("No such two sum solution");
    }
}
```
![result](https://img-blog.csdnimg.cn/20200305101608964.png)
