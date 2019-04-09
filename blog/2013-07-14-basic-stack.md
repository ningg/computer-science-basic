---
layout: post
title: 数据结构-栈
description: 自己实现一个栈
published: true
category: CS basic
---


## Java中基于数组实现的栈

定义一个数据结构所应满足的接口：*（增、删）*

	public class Stack {

		private Object[] stack;
		
		//元素个数;
		private int size;
		

		//默认长度为10;
		public Stack(){
			this(10);
		}
		
		//也可以自己设置长度,即容量;
		public Stack(int len){
			stack = new Object[len];
		}
		
		//返回元素个数;
		public int size(){
			return size;
		}
		
		//返回数组长度,即容量;
		public int capacity(){
			return stack.length;
		}
		
		//实现动态的数组;
		public void ensureCapacity(){
			if(size() == capacity()){
				Object[] newStack = new Object[size() * 3 / 2 + 1];
				System.arraycopy(stack, 0, newStack, 0, size());
				stack = newStack;
			}
		}
		
		//入栈;
		public void push(Object o){
			size++;
			ensureCapacity();
			stack[size - 1] = o;
		}
		
		
		//判空;
		public boolean isEmpty(){
			return size == 0;
		}
		
		//出栈;
		public Object pop(){
			//首先要判空;
			if(isEmpty()){
				throw new ArrayIndexOutOfBoundsException("不能为空");
			}
			
			Object o = stack[--size];
			stack[size] = null;
			return o;
		}
		
		
		
		
		
		public static void main(String[] args) {
			Stack stack = new Stack(3);
			String[] data = new String[] ;
			for (int i = 0; i < data.length; i++) {
					stack.push(data[i]);
					System.out.println(data[i] + "");
			}
			System.out.println("*****");
			while (!stack.isEmpty()) {
				System.out.println(stack.pop() + "");
			}
			//} 
		}
	} 


## Java中基于数组实现的队列


* [java 基于数组实现的队列][java 基于数组实现的队列]



##参考来源

* [用数组实现一个栈][用数组实现一个栈]
* [C语言一个栈的实现][C语言一个栈的实现]
* [java 基于单链表的实现的栈][java 基于单链表的实现的栈]
* [java 基于数组实现的队列][java 基于数组实现的队列]








[NingG]:    http://ningg.github.com  "NingG"


[打印1到最大的n位数]:			http://blog.csdn.net/zhaojinjia/article/details/8776639
[全排列和全组合实现]:			http://wuchong.me/blog/2014/07/28/permutation-and-combination-realize/#


[C语言一个栈的实现]:			http://blog.csdn.net/hopeyouknow/article/details/6725049
[用数组实现一个栈]:				http://zhidao.baidu.com/question/321517755.html?loc_ans=820812137
[java 基于单链表的实现的栈]:	http://blog.csdn.net/kingofase/article/details/5708624
[java 基于数组实现的队列]:		http://blog.csdn.net/kingofase/article/details/5708612

