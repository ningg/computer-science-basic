---
layout: post
title: 字符串转换为整数，整数转换为字符串
description: 全面考虑情况
published: true
category: CS basic
---


##字符串转换为整数


###基本逻辑

基本思路：逐个遍历字符，并且求出字符与`0`字符之间的差值，每次数字左移一位（十进制，就是乘以10）。

> 建议：下面代码，纸上重写时，使用`result`替代`num`会更有效果。

	int StringToInt(char* string)
	{
		if(string == null)
			return 0;

		int num=0;
		while(*string != '\0')
		{
			num *= 10;
			num += *string-'0';
			string++;
		}

		return num;
	}

几个问题：

* 输入字符串，带`+`\`-`号；
* 输入字符串，比较长，超过int范围；
	* C中int对应4字节，范围2的32次方*（4 x 10^9）*
	* long通常是8字节；
* 输入字符串，中间还有非法字符；





###考虑边界条件之后


	enum Status{ kValid = 0, kInValid };   //全局变量，标志字符串输入的状态：有效和无效
	int g_nStatus = kInValid;
	long long ConvertStrtoInt(const char *digit, bool minus);

	int StrtoInt(const char *str)
	{
		bool minus = false;        //标识字符串是否有“+”或“-”号

		long long num = 0;

		if(str != NULL && *str != '\0')
		{
			if(*str == '+')
				str++;
			else if(*str == '-')
			{
				minus = true;
				str++;
			}
			if(*str != '\0')     //字符串为非空字符时
			{
				num = ConvertStrtoInt(str,minus);
			}
		}
		return (int)num;
	}


	long long ConvertStrtoInt(const char *digit, bool minus)
	{
		long long num = 0;

		while(*digit != '\0')
		{

			if(*digit >= '0' && *digit <= '9')    //输入的字符应为数字，此时为有效输入
			{
				num = num*10 + (*digit - '0');    //字符串转换为整型数，注意正负数区别；此处须减去'0'，否则按阿拉伯数字字符的ASCII码表示。
				digit++;
			}
			else
			{
				num = 0;            //输入的字符为非法字符时，为无效输入
				break;
			}

		}

		if(*digit == '\0')  
		{
			g_nStatus = kValid;    //当输入字符串的最后一个字符为NULL时，此时输入为有效，其余的情况均为无效
			if(minus)
				num = 0 - num;
		}
		return num;
	}







##整数转换为字符串


十进制整数，转换为字符串：


char* intToString(int var)
{
	bool minus = false;
	if(var < 0)
	{
		minus = true;
		var = 0-var;
	}

	char buf[100];
	char* pointer = &buf[99];	// 避免buf中存储的字符串是倒序的
	*(pointer--) = '\0';

	while(var != 0)
	{
		*pointer= var % 10;
		pointer--;
		var /= 10;
	}

	if(minus){
		*pointer = '-';
		pointer--;
	}

	return pointer+1;
}



通用的写法：

	/*
	*    功能：整数转字符串
	*    @param int var 输入的整数
	*    @param int radix 转换进制 
	*    @return char * 返回转换后的字符串地址
	*/
	char *my_iota (int var, int radix)
	{
		static char local[33] = {0};    //考虑了32位二进制
		char *p = &local[32];
		static unsigned char table[] = "0123456789abcdef";

		bool sign = false;
		unsigned int tmp;
		if(radix < 2 && radix > 16)
		{
			*p = '\0';
			return p;
		}
		if(var < 0 && radix == 10)  //负整数转换十进制时，特殊处理
		{
			sign = true;
			var = -var;             
		}
		tmp = var;   //强制转化为无符号数,如var = -125 = 11111111 11111111 11111111 10000011,
					 //tmp = 11111111 11111111 11111111 10000011，此时首位1的含义已不同。

		*p-- = '\0';
		do{
			*p-- = table[tmp % radix]; 
			tmp /= radix;
		}while(tmp > 0);           //进制转换

		if(sign == true)           //负整数转换为十进制
		{
			*p-- = '-';
		}
		return p+1;
	}
















##参考来源

* [字符串转换整数及整数转换字符串][字符串转换整数及整数转换字符串]
* [C语言itoa()函数和atoi()函数详解(整数转字符C实现)][C语言itoa()函数和atoi()函数详解(整数转字符C实现)]









[NingG]:    http://ningg.github.com  "NingG"

[字符串转换整数及整数转换字符串]:						http://www.cnblogs.com/liu-jun/archive/2013/02/21/2921236.html
[C语言itoa()函数和atoi()函数详解(整数转字符C实现)]:		http://www.cnblogs.com/bluestorm/p/3168719.html













