title: "recursive symmetric tree"
date: 2015-05-21 17:23:58
tags:
- leetcode
- tech
---

> 提交递归 symmetric tree 代码的时候突然发现时间居然只要 4ms，比想像的还要好，所以又到了记录的时候了！

<!--more-->

# 思路
* 这是一棵树！  
  必须要有的想法，看到一棵树，递归！
* 这棵树是左右对称的  
  从左向右看 和 从右向左看 应该是一结果应该是一样的  
  
	> 这在突然想到，这样的话，就是从两边进行一个遍历再对比的过程，但是一个遍历结果并不能代表一棵树，会不会有问题呢？  
	> 很快就否定自己了，一个个比对的话，在对比的时候就确定了是相应的节点了，没有问题。
* 对比条件
	* 两个 NULL，真
	* 一个 NULL，一个非 NULL，假
	* 比较 value
		* value 不等，假
		* value 相等，递归进行两次比较
		
		```
		first->left, second->right
		first->right, second->left
		```
		返回两个递归比较和与。
* 边界条件
	* root == NULL 真
	
	
# 代码

```
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root == NULL)
            return true;
        return checkSymmetric(root->left, root->right);
    }
private:
    bool checkSymmetric(TreeNode *first, TreeNode *second){
        if(first == NULL && second == NULL)
            return true;        
        if(first == NULL ^ second == NULL)
            return false;
        if(first->val == second->val){
            return checkSymmetric(first->left, second->right) && checkSymmetric(first->right, second->left);
        }
        return false;
    }
};
```