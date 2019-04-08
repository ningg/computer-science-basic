---
layout: post
title: 位操作--二进制中1的个数
description: 统计一个整数对应二进制表示中1的个数
published: true
category: CS basic
---


> 实现一个函数，输入一个整数，输出该整数对应二进制表示中1的个数。


基本思路，对于二进制表示，直接右移，判断最低位是否为1，*（按位进行与`&`操作）*，即可；

	int Count(int n){
		int num = 0;
		while(n){
			if(n & 0x01)
				num++;
			n >>= 1;
		}
		return num;
	}

对于一个负整数，上述操作会陷入死循环；

Tips：

> 对于整数，左移`int << num`，最右端数字会补充为`0`；
> 
> 右移`int >> num`，需要针对正整数、负整数分别对待，对于正整数，右移时，最左端数字会补充为`0`；对于负整数，右移时，最左端会补充为`1`。

对于输入的整数为负整数时，可以不对输入的整数进行移位，而对`unsigned int flag = 1`进行移位操作。修改后代码为：

	int count(int n){
		int num = 0;
		unsigned int flag = 1;
		while(flag){
			if(n & flag){
				num++;
			}
			flag <<= 1;
		}
		
		return num;
	}

上述操作的时间复杂度，为`O(nlogn)`

更优的算法，时间复杂度为二进制中1的个数；这个需要利用规律了：把原始整数减去1，再和原始整数做`&`与运算，会将该整数的最右一个`1`变为`0`，那么，原始整数中，有多少个`1`，就可以进行多少次上述操作，代码如下：

	int count(int n){
		int num = 0;
		
		while(n){
			count ++1;
			n = (n-1) & n;
		}
		return num;
	}












[NingG]:    http://ningg.github.com  "NingG"