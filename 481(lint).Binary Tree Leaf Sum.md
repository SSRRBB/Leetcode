## 题目
Description
Given a binary tree, calculate the sum of leaves.

## 思路
method 1: 用DFS
但是有问题的话？？


method 2:不用DFS模板

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
        # 不加self 会怎么样, output = 0
        res = 0
        self.dfs(root, res)
        return res

    def dfs(self, root, res):
        if root is None:
            return
        #判断是否是叶子
        if root.left is None and root.right is None:
            res += root.val #这时候res新开地址了，导致下面两行调用时，仍然是就地址res=0
        self.dfs(root.left, res)
        self.dfs(root.right, res)

```

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
        
     ## 不加self 会怎么样, 用list []
        res = []
        self.dfs(root, res)
        return sum(res)

    def dfs(self, root, res):
        if root is None:
            return
        #判断是否是叶子
        if root.left is None and root.right is None:
            res.append(root.val)  #append不会新开地址
        self.dfs(root.left, res)
        self.dfs(root.right, res)

```
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
        
     ## Divide and Conquer（非dfs思想） 
        if not root:
            return 0

        if not root.left and not root.right:
            return root.val

        return self.leafSum(root.left) + self.leafSum(root.right)

```
