---
layout: post
title: 字符串--替换空格
description: 将字符串中指定字符，进行替换
published: true
category: CS basic
---


> 实现一个函数，将字符串中空格替换为`%20`，例如输入`We are happy.`，则，输出`We%20are%20happy.`。


基本思路，两个：

* 在原字符串上，进行替换；
* 新开辟存储空间，进行替换；


## 在原字符串上，进行替换


### 基本策略

基本策略：

* 扫描字符串，寻找空格字符
* 将空格字符的后续字符，后移2个空间*（char）*
* 将指定位置填充字符`%20`

假设字符长度为n，并且所有字符都是空格，则，时间复杂度`O(n^2)`。


### 提前扫描，一次分配，逆向复制

基本策略：

* 扫描一次字符串，统计出空格的个数
* 为原始字符串，分配空格数两倍的追加空间
* 使用两个指针，一个指向原字符串尾部、另一个指向新追加空间尾部
* 两个指针同时，逆向扫描并进行复制
* 两指针重叠时，终止

时间复杂度`O(n)`

### 示例代码

```
void ReplaceBlank(char* str, int len)  
{  
    if (len <= 0) 
        return; 
      
    int countBlank = 0;   
    //统计字符串中空格的个数  
    for (int i = 0; i <len; ++i)  
    {  
        if (str[i] ==' ' )  
        {  
            ++countBlank;  
        }  
    }
    if (0 == countBlank)  
        return; 
    
    int newLength = len + countBlank * 2;//计算新字符串长度  
    str.resize(newLength);//将字符串的容量一次性扩到新的大小    
    
    int oldIndex = len-1;//指向原始字符串结尾  
    int newIndex = newLength-1;//指向替换后字符串结尾  
    
    while (oldIndex>=0 && newIndex>oldIndex)  
    {  
        if (str[oldIndex] == ' ')  
        {  
            str[newIndex--] = '0';  
            str[newIndex--] = '2';  
            str[newIndex--] = '%';  
        }  
        else  
        {  
            str[newIndex--] = str[oldIndex];  
        }  
        --oldIndex;  
    }  
}
```


## 通用思路

合并两个数组/字符串时，如果从前往后复制每个数字，需要移动数字多次，则，考虑从后往前复制，减少移动次数，提高效率。





## 参考资料

* [ 请实现一个函数，把字符串中的每个空格替换成“20%”](http://blog.csdn.net/wanglelelihuanhuan/article/details/51648588)














[NingG]:    http://ningg.github.com  "NingG"









