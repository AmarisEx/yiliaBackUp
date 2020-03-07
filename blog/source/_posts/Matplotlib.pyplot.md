---
title:  Matplotlib.pyplot
date: 2020-02-16 12:39:04
tags:
	- python
	- matplotlib
---



- [matplotlib.pyplot](https://matplotlib.org/api/pyplot_api.html)
## 基本用法

```python
import matplotlib.pyplot as plt
import numpy as np
x = np.linspace(-1, 1, 50)
y = 2*x+1
plt.plot(x, y)
plt.show()
```
<!--more-->
![base](https://img-blog.csdnimg.cn/2020021522034991.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## figure 图像

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-1, 1, 50)
y1 = 2*x+1
y2 = x**2
plt.figure(num=1, figsize=(8, 5))
plt.plot(x, y1)
plt.figure()
plt.plot(x, y1, color='green', linestyle='--')
plt.plot(x, y2)
plt.show()
```
## 设置坐标轴

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-1, 1, 50)
y1 = 2*x+1
y2 = x**2

plt.figure()
plt.plot(x, y2)
plt.plot(x, y1, color='red', linewidth='3', linestyle='--')

plt.xlim((-1, 2))
plt.ylim((-2, 3))
plt.xlabel('x')
plt.ylabel('y')

new_ticks = np.linspace(-1, 2, 5)
plt.xticks(new_ticks)
#plt.yticks([-2, 0, 3], [r'bad$\alpha$', 'normal', 'good'])

# gca = 'get current axis'
ax = plt.gca()
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
ax.xaxis.set_ticks_position('bottom')
ax.yaxis.set_ticks_position('left')
ax.spines['bottom'].set_position(('data', 0))
ax.spines['left'].set_position(('data', 0))

plt.show()
```
![set axis](https://img-blog.csdnimg.cn/20200215224048716.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## Legend 图例

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-1, 1, 50)
y1 = 2*x+1
y2 = x**2

plt.figure()
plt.plot(x, y2, label='y=x^2')
plt.plot(x, y1, color='red', linewidth='2', linestyle='--', label='y=2x+1')

plt.xlim((-1, 2))
plt.ylim((-2, 3))
plt.xlabel('x')
plt.ylabel('y')

ax = plt.gca()
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
# ax.xaxis.set_ticks_position('bottom')
# ax.yaxis.set_ticks_position('left')
ax.spines['bottom'].set_position(('data', 0))
ax.spines['left'].set_position(('data', 0))

# Legend 图例
plt.legend(loc='best')

plt.show()
```
![legend](https://img-blog.csdnimg.cn/20200215225249963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## Annotation 标注

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-1, 1, 50)
y1 = 2*x+1
y2 = x**2

plt.figure()
# plt.plot(x, y2, label='y=x^2')
plt.plot(x, y1, color='red', linewidth='2', linestyle='--', label='y=2x+1')

plt.xlim((-1, 2))
plt.ylim((-2, 3))
plt.xlabel('x')
plt.ylabel('y')

ax = plt.gca()
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
# ax.xaxis.set_ticks_position('bottom')
# ax.yaxis.set_ticks_position('left')
ax.spines['bottom'].set_position(('data', 0))
ax.spines['left'].set_position(('data', 0))

# Legend 图例
plt.legend(loc='best')

# Annotation 标注
x0 = 0.5
y0 = 2*x0 + 1
plt.scatter(x0, y0, color='b', s=50)
plt.plot([x0, x0], [y0, 0], 'k--')

plt.annotate(r'$2x+1=%s$' % y0, xy=(x0, y0), xycoords='data', xytext=(+30, -30), textcoords='offset points',
             fontsize=16, arrowprops=dict(arrowstyle='->', connectionstyle='arc3, rad=.2'))
plt.text(-1, 1, r'$This\ is\ \alpha_t$', fontdict={'size': 16, 'color': 'r'})
plt.show()
```
![Annotation](https://img-blog.csdnimg.cn/20200216101543292.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## tick 能见度

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-3, 3, 50)
y = 0.1*x

plt.figure()
plt.plot(x, y, color='red', linewidth='2', linestyle='-', label='y=2x+1')

plt.xlim((-1, 2))
plt.ylim((-2, 3))
plt.xlabel('x')
plt.ylabel('y')

ax = plt.gca()
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')
# ax.xaxis.set_ticks_position('bottom')
# ax.yaxis.set_ticks_position('left')
ax.spines['bottom'].set_position(('data', 0))
ax.spines['left'].set_position(('data', 0))

# Legend 图例
plt.legend(loc='best')

# ticks 能见度
for label in ax.get_xticklabels() + ax.get_yticklabels():
    label.set_fontsize(12)
    label.set_bbox(dict(facecolor='white', edgecolor='None', alpha=0.7))

plt.show()
```
![ticks 能见度](https://img-blog.csdnimg.cn/20200216102320842.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## Scatter 散点图

```python
import matplotlib.pyplot as plt
import numpy as np

n = 2**10
x = np.random.normal(0, 1, n)
y = np.random.normal(0, 1, n)
T = np.arctan2(y, x)

plt.scatter(x, y, s=75, c=T, alpha=0.5)
plt.xlim(-1.5, 1.5)
plt.ylim(-1.5, 1.5)
plt.xticks(())
plt.yticks(())

plt.show()
```
![Scatter 散点图](https://img-blog.csdnimg.cn/20200216103015656.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## Bar 柱状图

```python
import matplotlib.pyplot as plt
import numpy as np

n = 12
x=np.arange(12)
y1 = (1-x/float(n)*np.random.uniform(0.5, 1, n))
y2 = (1-x/float(n)*np.random.uniform(0.5, 1, n))

plt.bar(x, y1, facecolor='#9999ff', edgecolor='white')
plt.bar(x, -y2, edgecolor='white')

for a, b in zip(x, y1):
    # plt.text(a - 0.4, b + 0.05, '%.2f' % b)
    plt.text(a, b, '%.2f' % b, ha='center')
for a, b in zip(x, y2):
    plt.text(a - 0.4, -b - 0.1, '%.2f' % b)

plt.show()
```

![Bar 柱状图](https://img-blog.csdnimg.cn/20200216104633775.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## Contours 等高线图

```python
import matplotlib.pyplot as plt
import numpy as np


def h(x, y):
    return (1 - x/2 + x**5 + y**3)*np.exp(-x**2-y**2)


n = 256
x = np.linspace(-3, 3, n)
y = np.linspace(-3, 3, n)
x, y = np.meshgrid(x, y)
plt.contourf(x, y, h(x, y), 8, alpha=0.75, cmap=plt.cm.hot)  # 热力图
C = plt.contour(x, y, h(x, y), 8, colors='black', alpha=0.6, linewidth=0.05)
plt.clabel(C, inline=True, fontsize=10)

plt.xticks(())
plt.yticks(())

plt.show()
```
![Contour 等高线图](https://img-blog.csdnimg.cn/20200216110654497.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## Image 图片

```python
import matplotlib.pyplot as plt
import numpy as np

a = np.random.random(16).reshape(4, 4)
print(a)

plt.imshow(a, interpolation='nearest', cmap='bone', origin='upper')
plt.colorbar(shrink=0.3)

plt.xticks(())
plt.yticks(())

plt.show()
```
![Image 图片](https://img-blog.csdnimg.cn/20200216111628491.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 3D 数据

```python
import matplotlib.pyplot as plt
import numpy as np
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure()
ax = Axes3D(fig)
x = np.arange(-4, 4, 0.25)
y = np.arange(-4, 4, 0.25)
x, y = np.meshgrid(x, y)
r = np.sqrt(x**2 + y**2)
z = np.sin(r)

ax.plot_surface(x, y, z, rstride=1, cstride=1, cmap=plt.get_cmap('rainbow'))

ax.contourf(x, y, z, zdir='z', offset=-2, cmap='rainbow')
ax.set_zlim(-2, 2)

plt.show()
```
![3D 数据](https://img-blog.csdnimg.cn/20200216113302867.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## subplot 多合一显示

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-np.pi, np.pi, 20)
y1 = np.sin(x)
y2 = np.cos(x)
y3 = np.tan(x)
y4 = np.exp(x)

plt.figure()

plt.subplot(211)
plt.plot(x, y1, label='y=sin(x)')
plt.legend(loc='best')

plt.subplot(234)
plt.plot(x, y2, label='y=cos(x)')
plt.legend(loc='best')

plt.subplot(235)
plt.plot(x, y3, label='y=tan(x)')
plt.legend(loc='best')

plt.subplot(236)
plt.plot(x, y4, label='y=exp(x)')
plt.legend(loc='best')

plt.show()
```
![subplot 多合一显示](https://img-blog.csdnimg.cn/2020021611433518.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 图中图

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-np.pi, np.pi, 20)
y = x.copy()
y1 = np.sin(x)
y2 = np.cos(x)

fig = plt.figure()

left, bottom, width, height = 0.1, 0.1, 0.8, 0.8
ax1 = fig.add_axes([left, bottom, width, height])
ax1.plot(x, y, 'r')
ax1.set_xlabel('x')
ax1.set_ylabel('y')
ax1.set_title('y=x')

left, bottom, width, height = 0.2, 0.6, 0.25, 0.25
ax2 = fig.add_axes([left, bottom, width, height])
ax2.plot(x, y1, 'r')
ax2.set_xlabel('x')
ax2.set_ylabel('y')
ax2.set_title('y=sin(x)')

plt.axes([0.6, 0.2, 0.25, 0.25])
plt.plot(x, y2, 'g')
plt.xlabel('x')
plt.ylabel('y')
plt.title('y=cos(x)')

plt.show()
```
![图中图](https://img-blog.csdnimg.cn/20200216120330603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## *次坐标轴

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-np.pi, np.pi, 20)
y1 = np.sin(x)
y2 = np.cos(x)

fig, ax1 = plt.subplots()
ax2 = ax1.twinx()  # 合并两个，镜面
ax1.plot(x, y1, 'g-')
ax2.plot(x, y2, 'b--')

ax1.set_xlabel('x')
ax1.set_ylabel('y1')

ax2.set_xlabel('x')
ax2.set_ylabel('y2')

plt.show()
```
![次坐标轴](https://img-blog.csdnimg.cn/20200216121551984.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## *Animation 动画

```python
import matplotlib.pyplot as plt
import numpy as np
from matplotlib import animation

fig, ax = plt.subplots()

x = np.arange(0, 2*np.pi, 0.01)
line, =ax.plot(x, np.sin(x))


def animate(i):
    line.set_ydata(np.sin(x+i/100))
    return line,


def init():
    line.set_ydata(np.sin(x))
    return line,


ani = animation.FuncAnimation(fig=fig, func=animate, frames=100, init_func=init, interval=20, blit=False)

plt.show()
```

