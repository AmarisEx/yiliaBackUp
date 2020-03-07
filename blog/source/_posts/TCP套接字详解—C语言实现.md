---
title:  Tcp套接字详解—C语言实现
date: 2020-01-05 19:00:21
tags:
	- 网络编程
---
# 基于C语言实现TCP套接字通信

> 本文旨在windows系统中使用TCP套接字实现客户端/服务端通信
> 编译器：visual studio 2019 (community)

Socket本意翻译为插座，这其实很形象的解释了套接字的作用，在客户端与服务端的通信中，套接字就起着像插座一样连接的作用。
TCP套接字与UDP套接字最大的区别便是是否面向连接，本文所实现的便是面向连接的TCP套接字，即客户端与服务端在通信之前进行三次握手建立连接。

<!-- more -->


## TCP服务端建立步骤：

 

 1. 申请套接字：s = socket(...);
 2. 确定本地端点，填写端点地址：address = ...;
 3. 建立套接字与端点关系（绑定）：bind(s,address...);
 4. 设置为监听模式：listen(s);
 5. 接收连接：newsock = accept(s);
 6. 数据收/发：recv(newsock); / send(newsock);
 7. 关闭套接字：closesocket(newsock);


## TCP客户端建立步骤：


 1. 申请套接字：s = socket(...);
 2. 确定本地端点，填写端点地址：c_address = ...;
 3. 建立套接字与端点关系（绑定)：bind(s,c_address...);
 4. 确定服务器端点：s_address = ...;
 5. 与服务器建立连接：connect(s,s_address...);
 6. 数据发/收：send(s); / recv(s);
 7. 关闭套接字：closesocket(s);

## TCP服务端代码实现

```cpp

#include <stdio.h>
#include <winsock2.h>
#include <time.h>
#include <stdlib.h>
#include <math.h>
#pragma comment(lib,"ws2_32.lib")

int main(int argc, char* argv[])
{
	//初始化WSA
	WORD sockVersion = MAKEWORD(2, 2);
	WSADATA wsaData;
	if (WSAStartup(sockVersion, &wsaData) != 0)
	{
		return 0;
	}

	//创建套接字
	SOCKET slisten = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
	if (slisten == INVALID_SOCKET)
	{
		printf("socket error !");
		return 0;
	}

	//绑定IP和端口
	sockaddr_in sin;
	sin.sin_family = AF_INET;
	sin.sin_port = htons(8888);
	sin.sin_addr.S_un.S_addr = INADDR_ANY;
	if (bind(slisten, (LPSOCKADDR)& sin, sizeof(sin)) == SOCKET_ERROR)
	{
		printf("bind error !");
	}

	//开始监听
	if (listen(slisten, 5) == SOCKET_ERROR)
	{
		printf("listen error !");
		return 0;
	}

	//循环接收数据
	SOCKET sClient;
	sockaddr_in remoteAddr;
	int nAddrlen = sizeof(remoteAddr);
	char revData[255];
	while (true)
	{
		printf("等待连接...\n");
		sClient = accept(slisten, (SOCKADDR*)& remoteAddr, &nAddrlen);
		if (sClient == INVALID_SOCKET)
		{
			printf("accept error !");
			continue;
		}
		printf("接受到一个连接：%s \r\n", inet_ntoa(remoteAddr.sin_addr));



		srand((unsigned)time(NULL));
		
		for (int i = 0; i <= 20; i++)
		{//接收数据
			int ret = recv(sClient, revData, 255, 0);
			//int my_revdata = int(*revData);// *（int* (const char*)revData)
			int my_revdata = *((int*)(revData));
			if (ret > 0)
			{
				revData[ret] = 0x00;
				//int b = int(*revData);
				//printf(revData);
				printf("成功接受数据：%3d", my_revdata);
			}

			//发送数据
			int randData = rand() % 500;
			randData = abs(randData);
			int my_sendData = my_revdata + randData;
			printf("我发送的数据：%5d \n", my_sendData);
			send(sClient, (const char*)(&my_sendData), sizeof(my_sendData), 0);
	
		}
		closesocket(sClient);
	}

	closesocket(slisten);
	WSACleanup();
	return 0;
}
```

## TCP客户端代码实现

```cpp

#include <WINSOCK2.H>
#include <STDIO.H>
#include <time.h>
#include <stdlib.h>
#include <math.h>
#include<windows.h>

#pragma  comment(lib,"ws2_32.lib")

int main(int argc, char* argv[])
{
	WORD sockVersion = MAKEWORD(2, 2);
	WSADATA data;
	if (WSAStartup(sockVersion, &data) != 0)
	{
		return 0;
	}

	SOCKET sclient = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
	if (sclient == INVALID_SOCKET)
	{
		printf("invalid socket !");
		return 0;
	}

	sockaddr_in serAddr;
	serAddr.sin_family = AF_INET;
	serAddr.sin_port = htons(8888);
	serAddr.sin_addr.S_un.S_addr = inet_addr("127.0.0.1");
	if (connect(sclient, (sockaddr*)& serAddr, sizeof(serAddr)) == SOCKET_ERROR)
	{
		printf("connect error !");
		closesocket(sclient);
		return 0;
	}


	srand((unsigned)time(NULL));
	for (int i = 0; i < 20; i++)
	{
		Sleep(500);
		int a = rand() % 500;
		a = abs(a);
		printf("我发送的随机数：%3d ", a);
		
		send(sclient, (const char*)(&a), sizeof(a), 0);
		char recData[255];
		int ret = recv(sclient, recData, 255, 0);
		int d = *((int*)(recData));
		if (ret > 0)
		{
			recData[ret] = 0x00;
			if (d > 100)
			{
				printf("成功接收返回数据：");
				printf("%5d\n", d);
			}
			else
			{
				printf("数据不符合要求！\n");
			}
		}

	}
	closesocket(sclient);
	WSACleanup();
	return 0;
}
```

