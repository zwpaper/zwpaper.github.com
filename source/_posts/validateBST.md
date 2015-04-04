title: "Validate Binary Search Tree"
date: 2015-04-04 14:44:58
tags: 
- tech
- leetcode
---

> 给定一棵二叉树，要判断是否二叉搜索树，一开始还觉得不麻烦，但是做起来突然发起也不顺手。。。

<!--more-->


# 题目

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

confused what "{1,#,2,3}" means? 

OJ's Binary Tree Serialization:
The serialization of a binary tree follows a level order traversal, where '#' signifies a path terminator where no node exists below.

Here's an example:

	   1
	  / \
	 2   3
	    /
	   4
	    \
	     5

The above binary tree is serialized as "{1,2,3,#,#,4,#,#,5}".

# 思路

* 一看到二叉搜索树的判定，直接就想到了来一个中根序就可以结束比赛了
* 因为有了上面的念头，于是开始想，有没有别的办法呢？直接来中根序好像太随意了，应该还有更好的方法的。。。
* 试了一下递归地比自己和自己的两个子节点，结果发现欠考虑了，比右子节点大，不代表比右子树都大！
* 刚好昨天 IDF 忙了一天，头有点大了，想不下去了，用了个 vector 把中根序存起来，实现了一下。
* 上网转了一圈，发现[水中的鱼](http://fisherlei.blogspot.com/2013/01/leetcode-validate-binary-search-tree.html)用了一个貌似挺不错的方法，有空得回头看一下，但是 Update 的那个用了 INT_MIN 和 INT_MAX, 在 [LeetCode 讨论](https://leetcode.com/discuss/14886/order-traversal-please-rely-buggy-int_max-int_min-solutions)上有人说这两个宏不能用得太随意，搜了一眼，没看到细节的东西，这个也得再了解一下
* [LeetCode 讨论](https://leetcode.com/discuss/14886/order-traversal-please-rely-buggy-int_max-int_min-solutions)中有个方法把中根序的做法合并了一下，直接记录上一个节点的引用，完成对中根序的比较，也是挺赞的，但是可惜时间复杂度上并没有太大的帮助


# Codes

自己的中根序比较

```
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isValidBST(TreeNode *root) {
        if( root == NULL )
        	return true;
        midOrder( root );
        return isOrdered( list );

    }
    std::vector<int> list;
    void midOrder( TreeNode *node )
    {
    	if( node == NULL )
    		return ;
    	midOrder( node->left );
    	list.push_back(node->val);
    	midOrder( node->right );

    }
    bool isOrdered(std::vector<int> &v)
    {
    	for(std::vector<int>::iterator i = v.begin(); ++i != v.end(); )
    	{
    		if( *i >= *(i + 1) )
    			return false;
    	}
    	return true;
    }
};
```

中根序合并

```
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isValidBST(TreeNode *root) {
    	TreeNode *p = NULL;
    	return inOrder( root, p );    
    }

    bool inOrder(TreeNode *node, TreeNode *prev)
    {
    	if( node == NULL )
    		return true;
    	if( !inOrder( node, node->left ) )
    		return false;
    	if(( prev != NULL )&&( node->val <= prev->val ))
    		return false;
    	return inOrder( node->right, node );
    }
};
```