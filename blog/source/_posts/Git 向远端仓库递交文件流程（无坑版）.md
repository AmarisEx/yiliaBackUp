---
title:  Git 向远端仓库递交文件流程（无坑版）
date: 2020-03-03 01:08:30
tags:
	- Git
	- Github
---

- **设置递交者信息**
	
	```bash
	git config -global user.name "yourname"
	git config -global user.email "your email"
	git config -list # 查看配置
	```
<!--more-->

- **添加所提交文件至本地仓库**

	```bash
	git add test.txt
	git commit -m "test"
	```
- **配置远端仓库**

	```bash
	git remote add origin https://test.github.com...
	git remote -v # 查看配置
	```
- **递交**

	```bash
	git branch # 查看当前所在分支
	git checkout master # 改变分支到master
	git push -u origin master # 假设你要提交到主分支master
	```

 	此过程会可能需要你登录你的github账号，按照提示做即可。
 	注意：最后会弹出一个窗口提示你填写目的仓库的用户名和密码，此处的密码是仓库所有者的**token**, 而非账号密码，token的获取可在settings中找到。
 	
