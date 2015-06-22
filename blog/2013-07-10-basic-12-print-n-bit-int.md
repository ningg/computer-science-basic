---
layout: post
title: 打印1到最大的n位数
description: 
published: true
category: CS basic
---



##参考来源

* [打印1到最大的n位数][打印1到最大的n位数]


如何进行全排列？全组合？






##全排列、全组合

* [全排列和全组合实现][全排列和全组合实现]

###全排列

基本思路：

* 第一位上，选出一个字符；
* 第二位上，选出一个剩余的字符；
* 依次类推，最后输出整个字符串；

代码层级，思路：

* 对任意一个排序，将第一位上的字符，与后面字符交换，即可产生新的排列；
* 对于子字符串，递归下去即可；





示例代码：



	//交换两个字符
	void Swap(char *a ,char *b)
	{
		char temp = *a;
		*a = *b;
		*b = temp;
	}

	//递归全排列，start 为全排列开始的下标， end 为str数组结束的下表
	void AllRange(char* str,int start,int end)
	{
		if(start == end)
		{
			printf("%s\n",str); // 输出整个字符串
		}
		else
		{
			for(int i=start; i<=end; i++)	
			{	
				//从下标为start的数开始，分别与它后面的数字交换
				Swap(&str[start],&str[i]); 
				AllRange(str,start+1,end);
				Swap(&str[start],&str[i]); 

			}
		}
	}


###全组合






















[NingG]:    http://ningg.github.com  "NingG"


[打印1到最大的n位数]:			http://blog.csdn.net/zhaojinjia/article/details/8776639
[全排列和全组合实现]:			http://wuchong.me/blog/2014/07/28/permutation-and-combination-realize/#





