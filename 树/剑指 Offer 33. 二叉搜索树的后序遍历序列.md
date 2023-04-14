## 题目描述
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”


## 解决思路
遍历树，用dict记录每个节点的父节点，root的父节点是它自己。

而后从p出发，沿着树遍历直到根节点，将经过的节点记录下来。

从q出发遍历到根，遇到的第一个在p->root路径上的节点即为最近公共祖先。


## 代码
```python
def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        def height(root:TreeNode,parent:TreeNode):
            if not root:
                return {}
            left={}
            if root.left:
                left.update(height(root.left,root))
            if root.right:
                left.update(height(root.right,root))
            left[str(root.val)]=parent
            return left
        dictt=height(root,root)
        np=p
        list_p=[np]
        while np!=root:
            np=dictt[str(np.val)]
            list_p.append(np)
        nq=q
        while nq not in list_p:
            nq=dictt[str(nq.val)]
        return nq


```
