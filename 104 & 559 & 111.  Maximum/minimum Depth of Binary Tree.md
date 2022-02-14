## 题目：104. Maximum Depth of Binary Tree
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.


Example 1:
```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```
Example 2:
```
Input: root = [1,null,2]
Output: 2
``` 
Constraints:
```
The number of nodes in the tree is in the range [0, 104].
-100 <= Node.val <= 100
```

## 思路：
BFS

DFS

## 答案：
**BFS**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        # res = 0
        res = []
        queue = collections.deque([root])
        
        while queue:
            level = []
            for _ in range(len(queue)):
                node = queue.popleft()
                level.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            res.append(level)
            # res += 1
        # return res
        return len(res)
                
                
```
**DFS recursion + 精简**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        return self.get_depth(root)
        
    def get_depth(self, root):
        if not root:
            return 0
        leftdepth = self.get_depth(root.left) #左
        rightdepth = self.get_depth(root.right) #右
        depth = max(leftdepth, rightdepth) + 1 #中
        return depth
```
```python
        if not root:
            return 0
        
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        return max(left_depth, right_depth) + 1
```

## 题目：559. Maximum Depth of N-ary Tree
https://leetcode.com/problems/maximum-depth-of-n-ary-tree/

## 答案：
**BFS**
```python
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        ## BFS
        if not root:
            return 0
        
        queue = collections.deque([root])
        res = 0
        
        while queue:
            for _ in range(len(queue)):
                node = queue.popleft()
                if node.children:
                    queue.extend(node.children) 
            res += 1     
        return res

```
**DFS**
```Python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
class Solution:
    def maxDepth(self, root: 'Node') -> int:
       ## DFS
        if not root:
            return 0
        depth = 0
        for i in range(len(root.children)):
            depth = max(depth, self.maxDepth(root.children[i]))
        return depth + 1

```
## 题目：111. Minimum Depth of Binary Tree
https://leetcode.com/problems/minimum-depth-of-binary-tree/

## 答案：
**BFS**
```python
    if not root:
            return 0
        
        queue = collections.deque([root])
        res = 0
        
        while queue:
            for _ in range(len(queue)):
                node = queue.popleft()
                if not node.left and not node.right:
                    return res + 1
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            res += 1
        return res

```

**DFS**
```python
 if not root:
            return 0
        if not root.left and not root.right:
            return 1
        min_depth = float('inf')
        if root.left:
            min_depth = min(self.minDepth(root.left), min_depth) # 获得左子树的最小高度
        if root.right:
            min_depth = min(self.minDepth(root.right), min_depth) # 获得右子树的最小高度
            
        return min_depth + 1

```
