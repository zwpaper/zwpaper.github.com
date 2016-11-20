title: "symmetric tree in leetcode"
date: 2015-05-21 17:23:58
tags:
- Leetcode
- Tech
---

> 提交递归 symmetric tree 代码的时候突然发现时间居然只要 4ms，比想像的还要好，所以又到了记录的时候了！

> 写了一个迭代算法了，也只用了4ms, 为什么提交记录里 C++ 用时都挺多，但是这我刚的这两个都只用 4ms 呢？


<!--more-->

# 递归
## 思路
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
	
	
## 代码

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

# 迭代
## 思路
* 左右对称的，那就一层层比较，每层是不是对称的，广度优先，BFS
* 非递归，用栈实现 BFS
* 每层在比对的时候需要空间保存节点，如果用支持随机访问的容器可以省空间
* 后面要加进来下一层的节点，前面要删除本层节点
* 结果出来了，**deque 双向队列**
* 各层比较
  * 记录当前层节点数
  * 每层头尾比较，包含 NULL
  * 两个都为 NULL，真
  * 两个都非 NULL，val 相等，真
  * 两个非 NULL，val 不等，假
  * 一个 NULL 一个非 NULL，假
  * 出现假直接返回就 OK
* 队列处理
  * 比较完一层，没有为假，把上层的节点出队
  * 出队的节点如果为 NULL，直接删除
  * 节点非 NULL，子节点入队（无论子节点是否为 NULL）
  * 按节点数出完队之后进行下一个循环
  * 循环跑完，则为真！
* 边界条件
  * root 为 NULL，先对 root 进行判断
  * 树中有 NULL 节点位置不同使得不对称树的某层非 NULL 节点对称，如：
    * 1 2 NULL 3 3 2 NULL 1
    * 如果只存非 NULL 节点，则是对称的
    * 所以 NULL 节点也要入队
		
		
## 代码
```
class Solution {
public:
	bool isSymmetric(TreeNode *root){
		if(root == NULL)
			return true;
		TreeNode *walker = NULL;
		int layer_size = 0;
		deque<TreeNode *> tree_deque;
		tree_deque.push_back(root->left);
		tree_deque.push_back(root->right);
		while(!tree_deque.empty()){
			layer_size = tree_deque.size();
			for(int i = 0; i < layer_size / 2; i++){
				if(tree_deque[i] == NULL ^ tree_deque[layer_size - 1 - i] == NULL) 
					return false;
				if(tree_deque[i] != NULL && tree_deque[layer_size - 1 - i] != NULL 
					&& tree_deque[i]->val != tree_deque[layer_size - 1 - i]->val )
					return false;
			}
			for(int i = 0; i < layer_size; i++){
				walker = tree_deque.front();
				tree_deque.pop_front();
				if(walker != NULL){
					tree_deque.push_back(walker->left);
					tree_deque.push_back(walker->right);
				}
			}
		}
		return true;
	}
};
```

