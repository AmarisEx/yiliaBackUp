---
title:  Hexo + gitee 创建个人博客网站
date: 2020-03-07 12:21:31
tags:
	- gitee
	- Hexo
---

# 写在前面
- 当你搜索Hexo + gitee 时，想必你已经用过了 github pages，也因为不能忍受其访问速度之慢而令求他法。
- 前期工作与本地部署请参见[基于Hexo框架搭建个人博客（windows)](https://blog.csdn.net/weixin_43488958/article/details/104572759)
- 相比较与github，**gitee**毕竟国产，访问速度自然不用多说，部署过程大致和github类似
<!--more-->
# 部署到Gitee详细流程
1. **创建新仓库**（切记以账号昵称命名）
![1](https://img-blog.csdnimg.cn/20200307115659986.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)这里的三个选项建议都选了，不然可能无法开启pages功能
![11](https://img-blog.csdnimg.cn/20200307115742229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
2. **pages开启**
打开**服务**下的**Gitee Pages**
![2](https://img-blog.csdnimg.cn/20200307115848153.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
进去之后什么都不用管，直接**启动**
![2](https://img-blog.csdnimg.cn/20200307120021978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
3. **远端部署**
	- **如果你之前用过github部署**，那么在此基础上只需要在根目录的_config.yml中将repository改成新的gitee的仓库即可
![git](https://img-blog.csdnimg.cn/20200307120327628.png)
**注意**：此处的地址并不是仓库地址，而是SSH或者http
![clone](https://img-blog.csdnimg.cn/202003071204533.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQ4ODk1OA==,size_16,color_FFFFFF,t_70)
大功告成！！！
	- **如果你没用过**，请参见[基于Hexo框架搭建个人博客（windows)](https://blog.csdn.net/weixin_43488958/article/details/104572759)中远端部署部分

