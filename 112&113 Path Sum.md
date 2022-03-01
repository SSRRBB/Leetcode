## 题目 112 path sum
Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.

A leaf is a node with no children.

 

Example 1:
```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
Output: true
Explanation: The root-to-leaf path with the target sum is shown.
```
Example 2:
```
Input: root = [1,2,3], targetSum = 5
Output: false
Explanation: There two root-to-leaf paths in the tree:
(1 --> 2): The sum is 3.
(1 --> 3): The sum is 4.
There is no root-to-leaf path with sum = 5.
```
Example 3:
```
Input: root = [], targetSum = 0
Output: false
Explanation: Since the tree is empty, there are no root-to-leaf paths.
```
Constraints:
```
The number of nodes in the tree is in the range [0, 5000].
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000
```
## 思路：

**path_sum + node.left.val隐形回溯**

BFS

DFS:这里的回溯指 利用 DFS 找出从根节点到叶子节点的所有路径，只要有任意一条路径的 和 等于 sum，就返True。
## 答案：
BFS
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        # BFS
        if not root:
            return False
        
        queue = collections.deque()
        queue.append((root, root.val))# 必须分开写
        
        while queue:
            node, path_sum = queue.popleft()
            if not node.left and not node.right and path_sum == targetSum:
                return True
            if node.left:
                queue.append((node.left, path_sum + node.left.val)) #path_sum + node.left.val隐形回溯
            if node.right:
                queue.append((node.right, path_sum+ node.right.val))
        return False

```
DFS
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        return self.dfs(root, targetSum, [root.val])
    
    def dfs(self, root, target, path):
        if not root:
            return False
        if not root.left and not root.right and sum(path) == target:
            return True
        
        left_flag, right_flag = False, False
        if root.left:
            left_flag = self.dfs(root.left, target, path + [root.left.val])
        if root.right:
            right_flag = self.dfs(root.right, target, path + [root.right.val])
        return left_flag or right_flag
```
