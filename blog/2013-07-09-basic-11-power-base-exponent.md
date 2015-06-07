---
layout: post
title: 边界条件--数值的整数次方
description: 功能、边界、异常的考虑
published: true
category: CS basic
---


> 实现函数：double Power(double base, int exponent)，求base的exponent次方。不需要考虑大数问题。



##忽略边界

示例：

	double Power(double base, int exponent)   
	{  
		  double result = 1.0;  

		  for(int i = 1; i <= exponent; ++i)  
				result *= base;  
	  
		  return result;  
	}  

##考虑边界，同时高效


更好的解法是基于下面的想法：


比如求X16,可以分解成：X16=X8*X8，于是，只要求出X8，再做一个乘积就可得到X16，同理，X8=X4*X4，……依次类推。所以求X16，只需要做4次乘积：X*X、X2*X2、X4*X4、X8*X8。如果用上面代码所述方法，要进行15次乘积。


现在问题变成，怎么把exponent分解成2的若干个整数次方，尤其是当exponent不是2的整数次方时，比如6。这里就用到了二进制的一些特点，比如6的二进制为0110，6可以分解为4+2，二进制熟悉的话，这里应该是一眼可以看出来的，就是对应二进制为1的位所表示的数的和。则X6=X4*X2。


作者也给出这种方法的一种实现，是比较容易理解的，用一个包含32个int的数组存储每一位对应的乘积，最终结果就是所有32个乘积的乘积。说得不清楚？结尾给你链接仔细去看……

	inline double power(double base, int exponent)  
	{  
		if(exponent <= 0)
			return 0;
		
		double tmp = base, result = 1.0;  
		for(int t=exponent; t>0; t/=2)  
		{  
			if(t%2==1) result*=tmp;  
			tmp = tmp * tmp;  
		}  
		return result;  
	}  


这几行代码做的事是一样的。t每次除以2表示t向右移动1位，t%2==1时，表示最右边的位为1，所以这里做的事是一样的。从t（也就是exponent）的二进制的最右边位（最低位）开始，如果为0，则不需要相乘，然后考虑第二位（通过移位实现），并且，这里用tmp来保存二进制中相应位对应的乘积，如果哪一位为1，刚把它乘到结果中去。



二进制的位，总是有一种无法言表的魅力：）








##参考来源

* [求某个数的整数次方][求某个数的整数次方]









[NingG]:    http://ningg.github.com  "NingG"


[求某个数的整数次方]:			http://blog.csdn.net/xianliti/article/details/5639606








