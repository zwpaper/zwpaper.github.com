title: "自增运算与 printf 参数顺序"
date: 2015-04-19 21:14:48
tags:
- tech
- C
---


> 最近找实习，做了两次笔记题发现，有些东西就是你不做题平时很难碰到的，于是乎，就把一直被人喷的 程序员面试宝典 搬出来研究一下。发现这题挺好玩的。

<!--more-->

# 原题目

What will be the output of the following C code?（ 以下代码的输出结果是什么？）
［中国著名通信企业 H 公司 2007 年 7 月面试题］ 

```
#include<stdio.h>
main()
{
	int arr[] = {6, 7, 8, 9, 10};
	int *ptr = arr;
	*(ptr++) += 123;
	printf("%d, %d\n", *ptr, *(ptr++));
}

```

## 原题解析

++ 运算相信大家都是知道的，直接到

		printf("%d, %d\n", *ptr, *(ptr++));

文章中这题的考点之一就在这里，好玩的地方也就是这里。

> printf("%d, %d\n", *ptr, *(++ptr))；  
> 从右到左运算，第一个是(++ptr)，也就是 ptr++，*ptr = 8, 此时 ptr 指向第三个元素 8， 所以全部为 8。

也就是说输出两个8.

===

===
# 分析

## OS X

OS X 中使用了 clang 作 C 编译器

> Apple LLVM version 6.0 (clang-600.0.57) (based on LLVM 3.5svn)

输出结果

> 7, 8

bingo~ 找到一个书上的错误

五毛 get~

但是真理之路往往不是这么一帆风顺的

## CentOS

刚好手头有个 CentOS 的机器，GCC 还是有的~于是乎

GCC 版本

> gcc version 4.4.7 20120313 (Red Hat 4.4.7-11) (GCC)

输出结果

> 8, 8

果然又是写书的，又是笔试题，还是不会全错的嘛~

但是你让考试的时候，又是用 OS X 的人情何以堪！！！

~~说不定这就是那59分里，被无辜扣的一分！~~

## Windows

手头没有 Windows 机器，查了一下

[这里](http://blog.csdn.net/bingxuewujian/article/details/6728396)
说是 VC6.0 中是从右到左的，但是他说的是在整个 printf 之后才会对 i 进行自增

那么，这道题又会出现一个答案

> 7， 7

兄弟，您确定吗？*对此持怀疑态度，有机会要试一下*

得放一放了，明天要面试，面试后更新。

---

# ToDo：

* VC / VS 中到底结果是怎么样的
* printf 在各系统中头文件实现
* 这个程序在各系统中输出的汇编是什么样子的