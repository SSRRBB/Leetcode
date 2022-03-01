## 题目 112 path sum
https://leetcode.com/problems/path-sum/
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
                queue.append((node.right, path_sum + node.right.val))
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
        return self.dfs(root, targetSum, root.val)
    
    def dfs(self, root, target, pathsum):
        if not root:
            return False
        if not root.left and not root.right and pathsum == target:
            return True
        
        left_flag, right_flag = False, False
        if root.left:
            left_flag = self.dfs(root.left, target, pathsum + root.left.val)
        if root.right:
            right_flag = self.dfs(root.right, target, pathsum + root.right.val)
        return left_flag or right_flag
        
```

## 题目 113 path sum II
https://leetcode.com/problems/path-sum-ii/

## 思路：
**隐形回溯path + [node.val], pathSum + node.left.val**
BFS

DFS

## 答案
BFS
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        # # BFS
        if not root:
            return []
        res = []
        queue = collections.deque()
        queue.append((root, [], root.val)) # 将要处理的节点，路径，路径和
        while queue:
            node, path, pathSum = queue.popleft()
            if not node.left and not node.right and pathSum == targetSum: # 如果是叶子节点,路径和等于sum
                res.append(path + [node.val]) # 保存路径 path + [node.val]这种做法类似257
            if node.left:
                queue.append((node.left, path + [node.val], pathSum + node.left.val)) 
            if node.right:
                queue.append((node.right, path + [node.val], pathSum + node.right.val))
        return res

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
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        #DFS
        res = []
        self.dfs(root, targetSum, res, [])
        return res

    def dfs(self, root, targetSum, res, path):
        if not root: # 空节点，不做处理
            return
        if not root.left and not root.right: # 叶子节点
            if targetSum == root.val: # 剩余的「路径和」恰好等于叶子节点值
                res.append(path + [root.val]) # 把该路径放入结果中
        self.dfs(root.left, targetSum - root.val, res, path + [root.val]) # 左子树
        self.dfs(root.right, targetSum - root.val, res, path + [root.val]) # 右子树

```

## 题目 257： Binary Tree Paths

**隐含回溯**

**如果把 path + "->"作为函数参数就是可以的，因为并有没有改变path的数值，执行完递归函数之后，path依然是之前的数值（相当于回溯了）**


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
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
            #BFS
        res = []
        queue = collections.deque([root])
        path_st = collections.deque([str(root.val)])

        while queue:
            node = queue.pop()
            path = path_st.pop()
            # 如果当前节点为叶子节点，添加路径到结果中
            if not node.left and not node.right:
                res.append(path)
            if node.left:
                queue.append(node.left)
                path_st.append(path + '->' + str(node.left.val))
            if node.right:
                queue.append(node.right)
                path_st.append(path + '->' + str(node.right.val))

        return res
        
```

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        # DFS 隐藏回溯
        if not root:
            return []
            
        res = []
        path = ''
        self.dfs(root, path, res)
        return res

    def dfs(self, root, path, res):
        path += str(root.val)
        
        if not root.left and not root.right:
            res.append(path)

        if root.left:
            # + '->' 是隐藏回溯
            self.dfs(root.left, path + '->', res)
        if root.right:
            self.dfs(root.right, path + '->', res) 
        return res

```
