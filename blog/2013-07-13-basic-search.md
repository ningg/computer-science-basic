---
layout: post
title: 搜索、查找
description: 二分查找、二叉搜索树查找
published: true
category: CS basic
---

几点：

* 二分查找：递归、非递归*（要求数组排序好）*
* 二叉搜索树查找
* Hash查找：空间换时间，`O(1)`的时间复杂度




##二分查找


简要说几点：

* 二分查找，针对已经排序好的数组
* 时间复杂度：`O(logn)`

###递归实现

递归方式，示例代码如下：

	int BinSearch(int Array[], int low, int high, int key/*要找的值*/)  
	{  
		if (low > high)
			return -1;
		
		int mid = (low+high)/2;  

		if(key == Array[mid])  
			return mid;  
		else if(key<Array[mid])  
			return BinSearch(Array,low,mid-1,key);  
		else if(key>Array[mid])  
			return BinSearch(Array,mid+1,high,key); 
 
	}  

Tips：

> 递归方式，基本思路：自顶向下，从后向前，迭代递归到收敛条件。

###非递归方式

示例代码如下：

	int BinSearch(int Array[], int low, int high, int key/*要找的值*/)  
	{  
		
		if(low > high)  // 异常
			return -1;
		
		int mid;  

		while (low<=high)  
		{  
			mid = (low+high)/2;  
			if(key==Array[mid])  
				return mid;  
			if(key<Array[mid])  
				high=mid-1;  
			if(key>Array[mid])  
				low=mid+1;  
		}  

		return -1;  
	}  

tips：

> 对于上述`(low+high)/2`可以改为移位操作，即`(low+high)>>1`


##二叉树查找

查找二叉排序树上是否有节点对应value值，示例代码如下：

	//查找以node为节点的树中上是否存在vlaue的节点  
	treeNode* searchTree(treeNode* node, int value){  

		if(node->value == value){  
				return node;  
		}else if(node->value > value){  
			if(node->left != NULL){  
					return searchTree(node->left, value);  
			}else{  
					return NULL;  
			}  
		}else{  
			if(node->right != NULL){  
					return searchTree(node->right, value);  
			}else{  
					return NULL;  
			}  
		}  
	}  



###维护一个二叉排序树

维护一个数据结构，要求实现针对这个数据结构的增、删、改、查，具体如下：


* [查找之二叉树查找][查找之二叉树查找]
















##参考来源


* [二分查找（递归与非递归）][二分查找（递归与非递归）]












[NingG]:    http://ningg.github.com  "NingG"

[二分查找（递归与非递归）]:		http://blog.csdn.net/q3498233/article/details/4419285
[查找之二叉树查找]:				http://blog.csdn.net/todd911/article/details/8471566







