# 题目描述
给定一个二叉树，原地将它展开为一个单链表。

例如，给定二叉树
```
    1
   / \
  2   5
 / \   \
3   4   6
```

将其展开为：
```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

# 解决思路
分治的思想：从题目要求的输出结果看，是将每个节点的左子树修改后的结果作为新的右子树，原右子树的处理结果后移，作为新生成的右子树最后一个叶子节点的右子树；

首先处理叶子节点和树为空的情况；

判断左子树是否为空，若不为空，则对其进行处理；判断右子树是否为空，若不为空，则需要将处理后的左子树作为新的右子树，并对原右子树进行处理，拼接到最后
；若右子树为空，则直接将处理后的左子树作为右子树即可；（这里需要注意的是要将原节点的左子树指向NULL）

若左子树为空，则只需要处理右子树，无需其他操作；


# 提交代码
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void flatten(TreeNode* root) {
        if(root==NULL ||(root->left==NULL && root->right==NULL)){
            return;
        }
        if(root->left!=NULL){
            flatten(root->left);
            if(root->right!=NULL){
                flatten(root->right);
                TreeNode* temp=root->right;
                root->right=root->left;
                root->left=NULL;
                TreeNode* u=root->right;
                while(u->right!=NULL){
                    u=u->right;
                }
                u->right=temp;
            }
            else{
                root->right=root->left;
                root->left=NULL;
            }
        }
        else{
            if(root->right!=NULL){
                flatten(root->right);
            }
        }
    }
};
```
