---
title:  图的遍历
date: 2020-02-10 20:36:48
tags:
	- 数据结构与算法
---



## 深度优先搜索
<!--more>

```c
/*图的遍历之深度优先搜索*/
#include<stdio.h>
int book[101],sum,n,e[101][101];
void dfs(int cur);//cur为当前所在顶点编号 

int main()
{
	int i,j;
	int m;
	printf("请输入顶点数n=");
	scanf("%d",&n);
	printf("\n请输入边数m=" );
	scanf("%d",&m);
	
	//邻接矩阵初始化 
	for(i=1;i<=n;i++)
	for(j=1;j<=n;j++)
	if(i==j) e[i][j]=0;
	else e[i][j]=99999999;
	
	printf("\n请输入顶点之间的边：\n");
	
	int a,b;
	for(i=1;i<=m;i++)
	{
		scanf("%d %d",&a,&b);
		e[a][b]=1;
		e[b][a]=1;
	 } 
	 
	 book[1]=1;
	 dfs(1);
	 
	getchar();getchar();
	return 0;
 } 
 void dfs(int cur)
 {
 	int i;
 	printf("当前顶点编号：%d\n",cur);
	sum++;
	if(sum==n)//判断是否访问结束 
	return;
	 for(i=1;i<=n;i++)
	 {
	 	if(e[cur][i]==1&&book[i]==0)
	 	{
	 		book[i]=1;
	 		dfs(i);
		 }
	  } 
	  return;
 }

```
## 广度优先搜索

```c
#include<stdio.h>
int main()
{
	int n,m;
	printf("请输入顶点数n=");
	scanf("%d",&n); 
	printf("请输入边数m=");
	scanf("%d",&m); 
	
	int e[101][101]={0};
	int i,j;
	for(i=1;i<=n;i++)
	for(j=1;j<=n;j++)
	if(i==j) e[i][j]=0;
	else e[i][j]=99999999;
	
	int a,b;
	printf("请输入顶点之间的边：\n");
	for(i=1;i<=m;i++)
	{
		scanf("%d %d",&a,&b);
		e[a][b]=1;
		e[b][a]=1;
	 } 
	 
	 int que[10001],book[101]={0};
	 int head,tail;
	 head=1;tail=1;//队列初始化 
	 
	 que[tail]=1;
	 tail++;
	 book[1]=1;
	 
	 int cur;
	 while(head<tail)
	 {
	 	cur=que[head];
	 	for(i=1;i<=n;i++)
	 	{
	 		if(e[cur][i]==1&&book[i]==0)
	 		{
	 			que[tail]=i;
	 			tail++;
	 			book[i]=1;
			}
			 if(tail>n)//判断是否遍历结束 
			 break;
	 	}
	 head++;//重要，扩展下一个点 
	 }
	 for(i=1;i<tail;i++)
	 printf("%d ",que[i]);
 } 

```

