title: "subsets in leetcode"
date: 2015-05-09 20:58:51
tags:
- Tech
- Leetcode
---

> 回朔法实践
 
<!--more-->
# 原题

```
Given a set of distinct integers, nums, return all possible subsets.

Note:
Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
For example,
If nums = [1,2,3], a solution is:

[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

# 解题思路

## 解决问题的基本思路

1. 明显例子的输出是刻意打乱了
2. 用一个小例子
3. 整理输出
4. 尝试推广

## 具体做法
* 1，2，3 作为小例子开始  
* 整理输出，可能的输出顺序应是：

	```
	1
	2
	3
	1 2
	1 3
	2 3
	1 2 3
	
	```
	用程序好像不容易实现
	既然是回朔法，那再试试
	
	```
	1
	1 2
	1 2 3
	1 3
	2
	2 3
	3
	```
	从这个输出能看出来，如果用递归，就可以从后面向前一点点组合
* Code

	```
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> result;
        vector<int> sets;
        result.push_back(sets);
        sort(nums.begin(), nums.end());
        for(int i = 0; i < nums.size(); i++)
            generater(result, nums, sets, i);
        return result;
    }
    void generater(vector<vector<int>> &output, vector<int> &resource, vector<int> sub, int index){
        if(index >= resource.size())
            return;
        sub.push_back(resource[index]);
        output.push_back(sub);
        for(int i = index + 1; i < resource.size(); i++){
            generater(output, resource, sub, i);
        }


    }
};	
	```
代码虽然不够漂亮，但这是自己一点点推出来的。

## 漂亮代码 
要找漂亮代码当然是 discuss 区！-> [这里](https://leetcode.com/discuss/questions/oj/subsets)

# 得失

## 得
* 培养自己一点点找思路，推出答案
* 开始理解 Backtracking 回朔法的概念

## 失

* 自己对算法还是很不熟悉，复杂一点的算法就容易没有思路

