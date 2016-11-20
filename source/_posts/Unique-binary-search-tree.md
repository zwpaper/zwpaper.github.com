title: "Unique binary search tree in LeetCode"
date: 2015-04-03 00:45:44
tags: 
- Tech
- Leetcode
---

> 最近时不时地刷一下 LeetCode，突然做了这么一道 Unique binary search tree，一看时间，尼码哥也有自豪的时候啦！快拿出来晒一晒~

<!--more-->
#Unique Binary Search Trees

[https://leetcode.com/problems/unique-binary-search-trees/]()

给一个数字，找出来能种多少棵搜索二叉树。

##思路

* 第一眼看到，卧槽，这什么奇皅题，上网找二叉搜索树是怎么建立的，别吐槽，都忘光了。。。
* 看了一下，没啥帮助啊，突然看到，为啥要给个3做例子呢？于是开始找规律，这货不就是节点都放左边，然后一个个挪到右边去么？
* 有规律了，再看看，没错了，就是这么挪，然后每挪一次，算出两边子树的个数，相乘，得到一种情况，再挪过去一个，再算，一直到一边的子树挪完了。
* 应该可以做了，来一个数字，开始递归算各个子树的值，再相乘相加
* 虽然之前做题的时候也用递归了，但是这个递归得有点狠啊，时间复杂度上不太好吧？想想有没有别的方法


## a

递归太狠，要改成递推！

啊！这不就是斐波那契数列么！

斐波那契数列有个递推的方法来着。。。

## aha Algrithm

19 个测试，1ms 的时间，C++ 比很多用 C 还快了~

Talk is cheap, show you the code!


```
class Solution {
public:
int numTrees(int n) {
	if( n <= 2 )
		return n;

	int numbers[n+1];
	numbers[0] = 1;
	numbers[1] = 1;

	int i,j;
	for( i = 2; i <= n; i++)
		numbers[i] = 0;
	for( i = 2; i <= n; i++ )
	{

		for( j = i - 1 ; j >=0; j-- )
		{
			numbers[i] += numbers[j] * numbers[i - j - 1];
		}
	}
    return numbers[n];
}
};
```

