---
title:  基于Hexo框架搭建个人博客（windows)
date: 2020-02-29 14:03:28
tags:
	- Hexo
	- git
	- github
---

---
# 环境准备
- [node.js](https://nodejs.org/en/download/)
- Git（git 官网下载很慢的，毕竟服务器在国外，可以去百度搜 Git 镜像）
<!--more-->
---
# 本地部署
( 建议所有命令均在 Git Bash 中执行）
![git vash](https://img-blog.csdnimg.cn/20200229131210261.png)

---
## SSH key 配置
1.  **$ cd ~/. ssh** 
检查本机已存在的ssh密钥
如果提示：No such file or directory 说明你是第一次使用git。
如果提示：bash: cd: too many arguments，此时可跳过第二步

2. **$ ssh-keygen -t rsa -C  "test@test.com"**
然后连续3次回车，最终会生成一个文件在用户目录下
3. 打开用户目录，找到**.ssh\id_rsa.pub**文件，记事本打开并复制里面的内容
![ssh](https://img-blog.csdnimg.cn/20200229131652732.png)
4. 打开你的github账号，在settings 中打开 SSH and GPG keys
![3](https://img-blog.csdnimg.cn/20200229131842234.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)然后 New SSH key, title自拟，将刚刚复制的内容复制到Key中，最后Add SHH key即可
![4](https://img-blog.csdnimg.cn/20200229132017824.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
----
## 本地配置
1. **检查nodejs是否安装成功**

	```css
	$ node -v
	$ npm -v
	```
	![test](https://img-blog.csdnimg.cn/20200229133041105.png)
2. **安装 Hexo**

	```css
	$ npm i -g hexo-cli
	```
3. **创建本地文件夹**
新建文件夹例如：blog
在该目录下打开 Git Bash 进行后续工作，以后所有的东西都会放在这个目录下
4. **初始化 Hexo**

	```css
	$ hexo init
	```
	![test](https://img-blog.csdnimg.cn/20200229133202436.png)
	此时，你会发现所在目录下多了很多文件
5. **安装主题**

	```css
	$ hexo g
	```
	![test](https://img-blog.csdnimg.cn/20200229133340742.png)
6. **测试本地服务**

	```css
	$ hexo s
	```
	![test](https://img-blog.csdnimg.cn/20200229133454611.png)
	浏览器打开 localhost:4000 可看到刚刚搭建的网站

---
## 更改主题
[yilia 主题](https://github.com/litten/hexo-theme-yilia)
yilia 是款很受欢迎的主题，就以它为例
1. **打开链接**，**复制其url** 
https://github.com/litten/hexo-theme-yilia.git

2.  **下载主题**

	```css
	$ git clone https://github.com/litten/hexo-theme-yilia.git /themes	/yilia
	```
3. **修改配置**

	```css
	$ vim _config.yml
	```
	进入配置文件，修改 theme 为 yilia
	![test](https://img-blog.csdnimg.cn/20200229134537989.png)
	(Esc + : wq 可退出)
4. **安装主题**
素质三连：

	```css
	$ hexo clean
	$ hexo g
	$ hexo s
	```
---
# 远端部署
当然，我们的博客不可能只在本地访问，因此我们需要部署到服务器或者免费的 Github Page 中
以下是部署到GitHub中的步骤
1. **创建 username.github.io**
新建仓库，以username.github.io命名，username务必使用你的账号昵称
2. **修改配置**

	```css
	$ vim _config.yml
	```
	![test](https://img-blog.csdnimg.cn/20200229135302642.png)
	修改为如图所示（账号仍使用自己的)
3. **发布**

	该过程中会需要你登陆账号，按着弹出的提示做就可以啦
	```css
	$ hexo d
	```
---
# 你的第一个博客网站
好了，到此就大功告成啦
个人觉得这样的主题看着满舒服的，接下来就是美化的工作了
![show](https://img-blog.csdnimg.cn/20200229135624930.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
