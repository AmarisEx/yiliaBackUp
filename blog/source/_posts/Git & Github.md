---
title:  Git & Github 入门
date: 2020-02-22 11:11:14
tags:
	- Git
	- Github
---


# Github
![test](https://img-blog.csdnimg.cn/20200221204225310.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- **Repository**
仓库,存放项目代码，类似文件夹
- **Star**
收藏
<!--more-->
- **Fork**
复制克隆项目
- **Pull Request**
发起请求：自己做了改进，请求合并
- **Watch**
关注，如果你Watch了某个项目，当该项目有变化会通知你
- **Issue**
事务卡片，发现代码Bug，但是目前没有成型代码，需要讨论时用

# Git
[Git 5分钟教程](https://www.runoob.com/w3cnote/git-five-minutes-tutorial.html)
## Git 工作区域
- **Git Repository** (Git 仓库)
最终确定的文件保存到仓库，成为一个新的版本，并且对他人可见
- **暂存区**
暂存已经修改的文件最后统一提交到git仓库中
- **工作区**（Working Directory）
添加、编辑、修改文件等动作
## 向仓库中添加文件流程
- git status 查看状况
- git add test.txt 从工作区提交到暂存区
- git status 查看状况
- git commit -m 暂存区提交到仓库
- git status


![1](https://img-blog.csdnimg.cn/20200221220525274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![2](https://img-blog.csdnimg.cn/20200221222452828.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![2](https://img-blog.csdnimg.cn/20200221222527833.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)

## 修改文件
![1](https://img-blog.csdnimg.cn/20200221223226844.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![2](https://img-blog.csdnimg.cn/20200221223401698.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## 删除文件
![1](https://img-blog.csdnimg.cn/20200221223610489.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
![2](https://img-blog.csdnimg.cn/2020022122363784.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
## Git管理远程仓库

- git config list : 查看配置
![git config list : 查看配置](https://img-blog.csdnimg.cn/20200222100541300.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
- git clone ... ：下载远端仓库
![git clone ... ：下载远端仓库](https://img-blog.csdnimg.cn/2020022210063952.png)- 提交文件到仓库...
- git push : 提交到远端
![git push : 提交到远端](https://img-blog.csdnimg.cn/20200222102541101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)

 
