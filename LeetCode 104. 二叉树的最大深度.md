# 题目描述
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，
```cpp
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

# 解决思路
DFS遍历输入的树，特别注意首先判断树是否为空，若为空，return 0;

若不为空，再判断从左右子节点（若存在）出发分别得到的路径长度，return更大的一个；

注意初始化路径长度为1，路径长度需要包含根节点；

# 提交代码
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        TreeNode *u;
        u=root;
        if(u==NULL){
            return 0;
        }
        if(u->left==NULL && u->right==NULL){ //reach leaf
            return 1;
        }
        int length_left=1;
        int length_right=1;
        if(u->left!=NULL){
            length_left+=maxDepth(u->left);
        }
        if(u->right!=NULL){
            length_right+=maxDepth(u->right);
        }
        if(length_left>length_right){
            return length_left;
        }
        else{
            return length_right;
        }
    }
};
```
