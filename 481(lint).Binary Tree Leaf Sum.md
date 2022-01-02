## 题目
Description
Given a binary tree, calculate the sum of leaves.

## 思路
用DFS

## 答案
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: the root of the binary tree
    @return: An integer
    """
    def leafSum(self, root):
        # write your code here
        self.res = 0 
        ##正常是用init函数定义类的属性，这里用self.也可以实现一样效果
        self.dfs(root)
        return self.res

    def dfs(self, root):
        if root is None:
            return
        #判断是否是叶子
        if root.left is None and root.right is None:
            self.res += root.val
        self.dfs(root.left)
        self.dfs(root.right)

```
