---
title:  Base64实现图片编解码
date: 2020-01-08 16:18:09
tags:
	- C
	- base64
---

- Base64是一种基于64个可打印字符来表示二进制数据的表示方法。
本文旨在通过base64对图片进行编解码，并可转换为8位2进制比特流，以实现图片文件在真实网络环境下的传输。
<!--more-->
## 主函数

```cpp
#include<stdio.h>
#include <stdlib.h>
#include<string.h>

unsigned int image_size_max = 100000;

//image
const char* base64char = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";
char* base64_encode(const unsigned char* bindata, char* base64, int binlength);
int base64_decode(const char* base64, unsigned char* bindata);
char* code_image(char* file_path);
void decode_image(char* imageBase64, unsigned int imageSize);
int main(int argc, char* argv[])
{
	//获取图片
	FILE* fp = NULL;
	char* file_path = NULL;
	file_path = (char*)malloc(64 * sizeof(char));
	printf("Please input your file path:");
	gets_s(file_path, 64);

	//图片编码
	char* image_ch = NULL;
	image_ch = (char*)malloc(image_size_max * sizeof(char));
	image_ch = code_image(file_path);
	printf("\n%s\n", image_ch);
	int image_size = strlen(image_ch);
	
	'''
	发方：image_ch-->>8位2进制比特流
	通过真实网络传输......
	收方：8位2进制比特流-->>image_ch
	//有关此部分内容的实现可查看笔者最小网元系列文章
	'''
	
	//图片解码
	decode_image(image_ch, image_size);//在当前目录下生成"outpuy.jpg"图片文件
	printf("\nover！\n");

	free(fp);
	free(file_path);
	free(image_ch);
	system("pause");
	return 0;
}
```

## base64字符库

 - 即base64表示的64个可打印字符

```cpp
const char* base64char = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";
```



## 图片编码函数

 - input：图片文件路径 
 - output：转换后的base64字符串

```cpp
char* code_image(char* file_path)
{
	FILE* fp = NULL;
	unsigned int imageSize;        //图片字节数
	char* imageBin;
	char* imageBase64;

	size_t result;
	char* ret;
	unsigned int base64StrLength;
	errno_t err;

	err = fopen_s(&fp, file_path, "rb");   //待编码图片
	if (NULL == fp)
	{
		printf("file open file");
		return 0;
	}
	//获取图片大小
	fseek(fp, 0L, SEEK_END);
	imageSize = ftell(fp);
	fseek(fp, 0L, SEEK_SET);

	//分配内存存储整个图片
	imageBin = (char*)malloc(sizeof(char) * imageSize);
	if (NULL == imageBin)
	{
		printf("malloc failed");
		return 0;
	}

	//读取图片
	result = fread(imageBin, 1, imageSize, fp);
	if (result != imageSize)
	{
		printf("file read failed");
		return 0;
	}
	fclose(fp);

	//分配编码后图片所在buffer
	imageBase64 = (char*)malloc(sizeof(char) * imageSize * 2);//因为编码一版会比源数据大1/3的样子，这里直接申请源文件一倍的空间
	if (NULL == imageBase64)
	{
		printf("malloc failed");
		return 0;
	}

	//base64编码
	base64_encode((const unsigned char*)imageBin, imageBase64, imageSize);
	base64StrLength = strlen(imageBase64);
	printf("base64 str length:%d\n", base64StrLength);
	printf("\ncode_pic->\n%s\n", imageBase64);
	return imageBase64;
}
```
## 图片解码函数

 - input：经base64编码后的字符串、字符串长度
 - output："output.jpg"（即解码后的图片）

```cpp
void decode_image(char* imageBase64, unsigned int imageSize)
{

	FILE* fp = NULL;
	//图片字节数
	char* imageBin;

	char* imageOutput;
	size_t result;
	char* ret;
	unsigned int base64StrLength;





	//分配存储解码数据buffer
	imageOutput = (char*)malloc(sizeof(char) * imageSize);//解码后应该和源图片大小一致
	if (NULL == imageBase64)
	{
		printf("malloc failed");
		//return -1;
	}
	base64_decode(imageBase64, (unsigned char*)imageOutput);
	errno_t err_1;
	err_1 = fopen_s(&fp, "output.jpg", "wb");
	if (NULL == fp)
	{
		printf("file open file");
		//return -1;
	}
	fwrite(imageOutput, 1, imageSize, fp);
	fclose(fp);

	//free(imageBin);
	free(imageBase64);
	free(imageOutput);


}
```
## base64编码函数

 - 在code_image中被调用

```cpp
char* base64_encode(const unsigned char* bindata, char* base64, int binlength)
{
	int i, j;
	unsigned char current;

	for (i = 0, j = 0; i < binlength; i += 3)
	{
		current = (bindata[i] >> 2);
		current &= (unsigned char)0x3F;
		base64[j++] = base64char[(int)current];

		current = ((unsigned char)(bindata[i] << 4)) & ((unsigned char)0x30);
		if (i + 1 >= binlength)
		{
			base64[j++] = base64char[(int)current];
			base64[j++] = '=';
			base64[j++] = '=';
			break;
		}
		current |= ((unsigned char)(bindata[i + 1] >> 4)) & ((unsigned char)0x0F);
		base64[j++] = base64char[(int)current];

		current = ((unsigned char)(bindata[i + 1] << 2)) & ((unsigned char)0x3C);
		if (i + 2 >= binlength)
		{
			base64[j++] = base64char[(int)current];
			base64[j++] = '=';
			break;
		}
		current |= ((unsigned char)(bindata[i + 2] >> 6)) & ((unsigned char)0x03);
		base64[j++] = base64char[(int)current];

		current = ((unsigned char)bindata[i + 2]) & ((unsigned char)0x3F);
		base64[j++] = base64char[(int)current];
	}
	base64[j] = '\0';
	return base64;
}
```
## base64解码函数

 - 在decode_image中被调用

```cpp
int base64_decode(const char* base64, unsigned char* bindata)
{
	int i, j;
	unsigned char k;
	unsigned char temp[4];
	for (i = 0, j = 0; base64[i] != '\0'; i += 4)
	{
		memset(temp, 0xFF, sizeof(temp));
		for (k = 0; k < 64; k++)
		{
			if (base64char[k] == base64[i])
				temp[0] = k;
		}
		for (k = 0; k < 64; k++)
		{
			if (base64char[k] == base64[i + 1])
				temp[1] = k;
		}
		for (k = 0; k < 64; k++)
		{
			if (base64char[k] == base64[i + 2])
				temp[2] = k;
		}
		for (k = 0; k < 64; k++)
		{
			if (base64char[k] == base64[i + 3])
				temp[3] = k;
		}

		bindata[j++] = ((unsigned char)(((unsigned char)(temp[0] << 2)) & 0xFC)) |
			((unsigned char)((unsigned char)(temp[1] >> 4) & 0x03));
		if (base64[i + 2] == '=')
			break;

		bindata[j++] = ((unsigned char)(((unsigned char)(temp[1] << 4)) & 0xF0)) |
			((unsigned char)((unsigned char)(temp[2] >> 2) & 0x0F));
		if (base64[i + 3] == '=')
			break;

		bindata[j++] = ((unsigned char)(((unsigned char)(temp[2] << 6)) & 0xF0)) |
			((unsigned char)(temp[3] & 0x3F));
	}
	return j;
}
```



