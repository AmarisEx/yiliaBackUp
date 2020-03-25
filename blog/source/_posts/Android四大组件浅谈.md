---
title:  Android四大组件浅谈
date: 2020-03-24 20:38:00
tags:
	- Android
---
`Activity`+`Service`+`BroadcastReciver`+`ContentProvider`
1. **Activity**
Activity就像一个响应事件，不过其响应的形式是可视化的界面，例如你现在所看到的窗体。Activity具有类似于树一样的层次关系，首先会有一个根Activity，其下可能会分多个子Activity。每个activity都 是Activity的子类。

<!--more-->
2. **Service**
Service是安卓系统的服务，其没有Activity一样的窗体，工作于后台，比如说我正在打字，可能就有Service在默默的统计字数。每一个service都扩展自类Serivce。
3. **BroadcastReciver**
BroadcastReciver是用来异步接收广播。同样的，它并没有界面，通常会从系统或者其他的应用中接收信息，然后会启动一个Activity进行响应，比如当手机来信息时就会有提示音这样。全部的接收器均继承自BroadcastReceiver基类。
4. **ContentProvider**
既然有Reciver肯定有相应的Provider，ContentProvider就是这样的存在。ContentProvider会提供一些特定的应用程序数据共享给其他应用，就比如微信可以获得我们手机联系人的信息一样（当然，这需要权限）。内容提供者继承于ContentProvider 基类
---
总的来说，这四大组件之间通过一定的逻辑关系相互关联，是安卓开发的必要组成。


