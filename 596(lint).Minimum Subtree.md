## 题目：
Description
Given a binary tree, find the subtree with minimum sum. Return the root of the subtree.
The range of input and output data is in int.

LintCode will print the subtree which root is your return node.
It's guaranteed that there is only one subtree with minimum sum and the given binary tree is not an empty tree.
Example
Example 1:
```
Input:
{1,-5,2,1,2,-4,-5}
Output:1
Explanation:
The tree is look like this:
     1
   /   \
 -5     2
 / \   /  \
1   2 -4  -5 
The sum of whole tree is minimum, so return the root.
```
Example 2:
```
Input:
{1}
Output:1
Explanation:
The tree is look like this:
   1
There is one and only one subtree in the tree. So we return 1.
```

![p](https://github.com/SSRRBB/Leetcode/blob/main/Images/100.png)

## 思路：
DFS
分治法


![p](https://github.com/SSRRBB/Leetcode/blob/main/Images/101.png)

## 答案：
**全局变量的分治法**
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
    @param root: the root of binary tree
    @return: the root of the minimum subtree
    """
    ##使用了全局变量
    def findSubtree(self, root):
        # write your code here
        #最小和初始值为无穷大
        self.minimum_weight = float('inf')
        #最小和子树根节点
        self.minimum_subtree_root = None

        self.getTreeSum(root)

        return self.minimum_subtree_root

    #得到 root为根的二叉树的所有节点之和
    #顺便打擂台求出minimum subtrem
    #递归三要素之一：递归的定义
    def getTreeSum(self, root):
        #递归三要素之二：递归的出口
        if root is None:
            return 0

        #递归三要素之三：递归的拆解
        #左子树之和
        left_weight = self.getTreeSum(root.left)
        #右子树之和
        right_weight = self.getTreeSum(root.right)
        #当前树之和
        root_weight = left_weight + right_weight + root.val

        # 如果当前树之和更小，更新最小和，以及最小和节点
        if root_weight < self.minimum_weight:
            self.minimum_weight = root_weight
            self.minimum_subtree_root = root

        #返回当前和
        return root_weight
    


```
**无全局变量的分治法**
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
    @param root: the root of binary tree
    @return: the root of the minimum subtree
    """
    def findSubtree(self, root):
        
        minimum, subtree, sum_of_root = self.helper(root)
        return subtree

    #返回  最小和， 最小子树根， 当前数之和，
    def helper(self, root):
        # 递归出口
        if root is None:
            return sys.maxsize, None, 0
        
        #左子树之和
        left_minimum, left_subtree, left_sum = self.helper(root.left)
        #右子树之和
        right_minimum, right_subtree, right_sum = self.helper(root.right)
        #当前子树之和
        sum_of_root = left_sum + right_sum + root.val
        #如果左子树最小，返回左子树
        if left_minimum == min(left_minimum, right_minimum, sum_of_root):
            return left_minimum, left_subtree, sum_of_root
        if right_minimum == min(left_minimum, right_minimum, sum_of_root):
            return right_minimum, right_subtree, sum_of_root
    
        #如果当前树最小，返回当前树
        return sum_of_root, root, sum_of_root
```
