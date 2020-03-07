---
title:  Python 爬虫基础教程
date: 2020-02-17 10:45:51
tags:
	- python
	- 爬虫
---



## 爬取网页流程
1. 选择网址（url）
2. 使用 python 登录上这个网址 (urlopen) 等
3. 读取网页信息
4. 将读取的信息放入 BeautifulSoup
5. 使用 BeautifulSoup 选取 tag 信息等（代替正则表达式）
<!-- more -->
## 了解网页结构
-  $<html>,</html>$首尾
- $<head>,</head>$头部，不显示
- $<body>,</body>$主体

```html
<!DOCTYPE html>
<html lang="cn">
<head>
	<meta charset="UTF-8">
	<title>Scraping tutorial 1 | 莫烦Python</title>
	<link rel="icon" href="https://morvanzhou.github.io/static/img/description/tab_icon.png">
</head>
<body>
	<h1>爬虫测试1</h1>
	<p>
		这是一个在 <a href="https://morvanzhou.github.io/">莫烦Python</a>
		<a href="https://morvanzhou.github.io/tutorials/scraping">爬虫教程</a> 中的简单测试.
	</p>

</body>
</html>
```
- **python 匹配网页源码**

```python
from urllib.request import urlopen

html = urlopen(
    "https://morvanzhou.github.io/static/scraping/basic-structure.html"
).read().decode('utf-8')
print(html)


import re
res = re.findall(r"<title>(.+?)</title>", html)
print("\nPage title is: ", res[0])

res = re.findall(r"<p>(.*?)</p>", html, flags=re.DOTALL)    # re.DOTALL if multi line
print("\nPage paragraph is: ", res[0])

res = re.findall(r'href="(.*?)"', html)
print("\nAll links: ", res)
```
## BeautifulSoup 解析网页：基础
- 安装（windows下）：pip install beautifulsoup4

```python
from urllib.request import urlopen
from bs4 import BeautifulSoup

html = urlopen(
    "https://morvanzhou.github.io/static/scraping/basic-structure.html"
).read().decode('utf-8')
# print(html)

soup = BeautifulSoup(html, features='lxml')
# print(soup.h1)
# print('\n', soup.p)

all_href = soup.find_all('a')
for l in all_href:
    print(l['href'])
```
![href](https://img-blog.csdnimg.cn/20200216195441110.png)
## BeautifulSoup 解析网页：CSS
![test](https://img-blog.csdnimg.cn/20200216201801125.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
```python
from urllib.request import urlopen
from bs4 import BeautifulSoup

html = urlopen(
    "https://morvanzhou.github.io/static/scraping/list.html"
).read().decode('utf-8')
# print(html)

soup = BeautifulSoup(html, features='lxml')

# month = soup.find_all('li', {'class': 'month'})
# for m in month:
#     print(m.get_text())

jan = soup.find('ul', {'class': 'jan'})
print(jan)
d_jan = jan.find_all('li')
for d in d_jan:
    print(d.get_text())
```

![result](https://img-blog.csdnimg.cn/20200216201819628.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## BeautifulSoup 解析网页：正则表达式
- [BeautifulSoup 解析网页：正则表达式](https://morvanzhou.github.io/tutorials/python-basic/basic/13-10-regular-expression/)
## 爬百度百科
 error


```python
from bs4 import  BeautifulSoup
from urllib.request import urlopen
import re
import random

base_url = "https://baike.baidu.com/"
his = ["/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB/5162711"]

for i in range(3):
    url = base_url + his[-1]

    html = urlopen(url).read().decode('utf-8')
    soup = BeautifulSoup(html, features='lxml')
    print(i, soup.find('h1').get_text(), '    url: ', his[-1])

    # find valid urls
    sub_urls = soup.find_all("a", {"target": "_blank", "href": re.compile("/item/(%.{2})+$")})

    if len(sub_urls) != 0:
        his.append(random.sample(sub_urls, 1)[0]['href'])
    else:
        # no valid sub link found
        his.pop()
```
## Post 登录 Cookies(Requests)
- 其实在加载网页的时候, 有几种类型, 而这几种类型就是你打开网页的关键. 最重要的类型 (method) 就是 get 和 post (当然还有其他的, 比如 head, delete). 刚接触网页构架的朋友可能又会觉得有点懵逼了. 这些请求的方式到底有什么不同? 他们又有什么作用?

- 我们就来说两个重要的, get, post, 95% 的时间, 你都是在使用这两个来请求一个网页.

-    **post**
        账号登录
        搜索内容
        上传图片
        上传文件
        往服务器传数据 等
-    **get**
        正常打开网页
        不往服务器传数据


```python
import requests
import webbrowser

# param = {"wd": "莫烦Python"}
# r = requests.get('https://www.baidu.com/s', params=param)
# print(r.url)

# data = {'firstname': 'Guosheng', 'lastname': 'Zhang'}
# r = requests.post('http://pythonscraping.com/files/processing.php', data=data)
# print(r.text)

# file = {'uploadFile': open('./image.png', 'rb')}
# r = requests.post('http://pythonscraping.com/files/processing2.php', files=file)
# print(r.text)
```

