---
layout: post
title: 打印1到最大的n位数
description: 
published: true
category: CS basic
---



## 参考来源

* [打印1到最大的n位数][打印1到最大的n位数]

如何进行全排列？全组合？

## 全排列、全组合

* [全排列和全组合实现][全排列和全组合实现]
* [java 全组合 与全排列](http://www.cnblogs.com/lifegoesonitself/p/3225803.html)

### 全排列

Tips:

> 1. 所有元素, 都需要出现
> 2. 不同元素, 有顺序

基本思路：

* 第一位上，选出一个字符；
* 第二位上，选出一个剩余的字符；
* 递归，最后输出整个字符串；

代码层级，思路：

* 对任意一个排序，将第一位上的字符，与后面字符交换，即可产生新的排列；
* 对于子字符串，递归下去即可；

示例代码：

    /**
     * 获取输入数组的全排列
     *
     * @param array 输入的数组
     * @param result 已经排列的数组
     */
    public static void allRange(String array, String result) {

        // 1. 边界判断
        if (null == array) {
            return;
        }

        int length = array.length();
        int currLength = result.length();

        // 2. 终止条件
        if (currLength == length) {
            System.out.println(result);
        }

        // 3. 迭代: 不满足条件的分支, 不进行后续处理, 相当于'剪枝'
        for (int i = 0; i < array.length(); i++) {
            if (result.indexOf(array.charAt(i)) < 0) {
                allRange(array, result + array.charAt(i));
            }
        }
    }


### 全组合

基本思路：求全组合，则假设原有元素n个，则最终组合结果是2^n个。

原因是：

* 用位操作方法：假设元素原本有：a,b,c三个，则1表示取该元素，0表示不取。故去a则是001，取ab则是011.
* 所以一共三位，每个位上有两个选择0,1.所以是2^n个结果。
* 这些结果的位图值都是0,1,2....2^n。

所以从值0到值2^n依次输出结果：即：

* 000,001,010,011,100,101,110,111 。

对应输出组合结果为：

* 空,a, b ,ab,c,ac,bc,abc.

这个输出顺序刚好跟数字0~2^n结果递增顺序一样, 取法的二进制数其实就是从0到2^n-1的十进制数。

对应的代码:

```
    public static void combination(String[] strArray) {
        // 1.边界判断
        if (null == strArray) {
            return;
        }

        // 2. 基础准备
        int len = strArray.length;
        int bitMax = 1 << len;

        // 3. 逐个数字, 获取二进制表示格式, 并获取对应的排列
        for (int index = 0; index < bitMax; index++) {
            StringBuffer strBuffer = new StringBuffer();
            for (int currBit = 0; currBit < len; currBit++) {
                int currValue = (1 << currBit);
                if ((index & currValue) != 0) {
                    strBuffer.append(strArray[currBit]);
                }
            }
            System.out.println(strBuffer);
        }

    }
```




[NingG]:    http://ningg.github.com  "NingG"


[打印1到最大的n位数]:			http://blog.csdn.net/zhaojinjia/article/details/8776639
[全排列和全组合实现]:			http://wuchong.me/blog/2014/07/28/permutation-and-combination-realize/#