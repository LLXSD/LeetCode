# 题目描述
在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

示例 1:
```
输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
```
示例 2:
```
输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
```

# 解决思路
动态规划：每个节点有选择和不选择两种可能，如果选择当前节点，那么其子节点就不能被选择；如果不选择当前节点，那么其子节点可以选择或不选择；

两种状态下节点i对应的收益计算方式如下，其中0表示不选择，1表示选择：
```
revenue_1[i]=i.val+revenue_0[i.left]+revenue_0[i.right];
revenue_0[i]=max(revenue_0[i.left],revenue_1[i.left])+max(revenue_0[i.right],revenue_1[i.right]);
```
面临的问题是需要一个合适的数据结构可以存储上述收益，如果利用数组结构，树中节点下标计算相对比较复杂；根据官方给出的题解，得知unordered_map此种数据结构，哈希表；
使用哈希表可以实现key-value映射，并且可以指定数据类型，是一种比较好的选择；

在学习官方代码时，存在疑问的点在于哈希表如何保证映射不冲突，这部分知识将会在调查学习后补充在这里。

# 进一步思考
如果这道题目要求输出被打劫的房舍的单个的价值，应该怎么办？

添加方法df1，自上而下从根节点开始遍历二叉树，打印相关价值信息：

```cpp
void dfs1(TreeNode* o, int flag) {
        if (!o) {
            return;
        }
        if(f[o]>g[o] && flag==0){
            cout<<o->val<<endl;
            dfs1(o->left,1);
            dfs1(o->right,1);
        }else{
            dfs1(o->left,0);
            dfs1(o->right,0);
        }
    }
```

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
    unordered_map <TreeNode*, int> f, g;
    //哈希表初始化
    void dfs(TreeNode* o) {
        if (!o) {
            return;
        }
        dfs(o->left);
        dfs(o->right);
        f[o] = o->val + g[o->left] + g[o->right];
        g[o] = max(f[o->left], g[o->left]) + max(f[o->right], g[o->right]);
    }

    int rob(TreeNode* o) {
        dfs(o);
        return max(f[o], g[o]);
    }
};
```
