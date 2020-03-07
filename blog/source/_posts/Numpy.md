---
title:  Numpy
date: 2020-02-15 21:51:47
tags:
	- python
	- numpy
---

- [numpy](https://docs.scipy.org/doc/numpy/reference/index.html)
## numpy属性

```python
import numpy as np
import torch
array = np.array([[1, 2], [3, 4]])
print(array.shape)
print(array.size)
array = torch.from_numpy(array)
print(array.size(-1))
```
<!--more-->
## numpy的创建array

```python
import numpy as np
import torch

# a = np.array([[1, 2], [3, 4]], dtype=np.float64)
# print(a.dtype)

# b = np.zeros((3, 4), dtype=np.float)
# c = np.ones((3, 4), dtype=np.int)
# d = np.eye(2, dtype=int)
# e = np.empty((3, 4))
# print(b)
# print(c)
# print(d)
# print(e)

# a = np.arange(10, 20, 2)
# a = np.arange(12).reshape((3, 4))
a = np.linspace(1, 10, 20)
print(a)
```
## numpy的基本运算

```python
import numpy as np

# a = np.linspace(10, 40, 4)
# b = np.arange(4)
# print(a*b)
# c = b**2
# print(b < 2)

# a = np.arange(4).reshape((2, 2))
# b = np.arange(5, 9).reshape((2, 2))
# print(a)
# print(b)
# print(a*b)
# print(np.dot(a, b))  # 矩阵运算
# print(a.dot(b))  # 矩阵运算

# a = np.random.random((2, 4))
# print(a)
# print(np.max(a, 1))

# a = np.arange(2, 14).reshape((3, 4))
# print(np.mean(a))
# print(np.average(a))
# print(np.median(a))

a = np.random.random((2, 3))*10
print(np.sort(a))
print(np.transpose(a))
```
## numpy的索引

```python
import numpy as np

a = np.arange(3, 15).reshape((3, 4))
print(a)
# print(a[2, 3])
# print(a[:, 1])
# print(a[1, 1:3])

# for row in np.transpose(a):
#     print(row)

# print(a.flatten())
# for i in a.flat:
#     print(i)
```
## numpy array 合并

```python
import numpy as np

a = np.random.random(3)
b = np.random.random(3)
# print(np.vstack((a, b)))  # vertical stack
# print(np.hstack((a, b)))  # horizontal stack
# print(np.vstack((a, b)).shape)

print(a.shape)
print(a[np.newaxis, :].shape)
```
## numpy array 分割

```python
import numpy as np

a = np.arange(12).reshape((3, 4))
print(a)
# print(np.split(a, 3, 0)[0])  # 等量分割
# print(np.array_split(a, 3, 1))  # 非等量分割

print(np.hsplit(a, 2))
print(np.vsplit(a, 3))
```
## numpy 的 copy & deep copy

```python
import numpy as np

a = np.arange(4)
b = a
c = a.copy()
a[0] = 3
print(a)
print(b)  # copy 类似引用，地址一样
print(c)  # deep copy
```

