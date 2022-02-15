## 题目：100. Same Tree & 101. Symmetric Tree

https://leetcode.com/problems/same-tree/

https://leetcode.com/problems/symmetric-tree/

## 思路：
Recursion

iteration(BFS)

## 答案：100. Same Tree
**Recursion**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # recursion
        return self.compare(p, q)
    
    def compare(self, p, q):
        if not p and not q:
            return True
        if not p and q:
            return False
        if p and not q:
            return False
        if p.val != q.val:
            return False
        
        leftsame = self.compare(p.left, q.left)
        rightsame = self.compare(p.right, q.right)
        isSame = leftsame and rightsame
        return isSame

```
**iteration(BFS)**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
       # iteration BFS  # 同时遍历两棵树，分类讨论各种情况。
        if not p and not q:
            return True
         
        queue1 = collections.deque([p])
        queue2 = collections.deque([q])
        while queue1 and queue2:
            node1 = queue1.popleft()
            node2 = queue2.popleft()
            # 如果都是空节点，跳过
            if not node1 and not node2:
                continue   
            # 如果有一个为空，不可能相等，返回false
            if not node1 and node2 or node1 and not node2:#if not node1 or not node2
                return False
            # 如果不为空，一定有值，若不相等，直接返回false。若相等，再后续添加节点
            if node1.val != node2.val:
                return False
            queue1.append(node1.left)
            queue1.append(node1.right)
            queue2.append(node2.left)
            queue2.append(node2.right)
        # 如果还有节点没遍历完，则一定不等
        if queue1 and queue1:
            return False
        return True
 

```
## 答案：101. Symmetric Tree
**Recursion**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        # recursion
        if not root:
            return True
        return self.compare(root.left, root.right)
        
    def compare(self, left, right):
        #首先排除空节点的情况
        if left == None and right == None: 
            return True
        if left == None and right != None: 
            return False
        if left != None and right == None: 
            return False
        #排除了空节点，再排除数值不相同的情况
        if left.val != right.val: 
            return False
        
        #此时就是：左右节点都不为空，且数值相同的情况
        #此时才做递归，做下一层的判断
        outside = self.compare(left.left, right.right) #左子树：左、 右子树：右
        inside = self.compare(left.right, right.left) #左子树：右、 右子树：左
        isSame = outside and inside #左子树：中、 右子树：中 （逻辑处理）
        return isSame

```

**iteration**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        # iteration
        if not root:
            return True
        queue = collections.deque()
        queue.append(root.left) #将左子树头结点加入队列
        queue.append(root.right) #将右子树头结点加入队列
        while queue: #接下来就要判断这这两个树是否相互翻转
            leftNode = queue.popleft()
            rightNode = queue.popleft()
            if not leftNode and not rightNode: #左节点为空、右节点为空，此时说明是对称的
                continue
            
            #左右一个节点不为空，或者都不为空但数值不相同，返回false.若相等，再后续添加节点
            if not leftNode or not rightNode or leftNode.val != rightNode.val:
                return False
            queue.append(leftNode.left) #加入左节点左孩子
            queue.append(rightNode.right) #加入右节点右孩子
            queue.append(leftNode.right) #加入左节点右孩子
            queue.append(rightNode.left) #加入右节点左孩子
        return True

```
