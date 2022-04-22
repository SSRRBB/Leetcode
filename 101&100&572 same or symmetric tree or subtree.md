## 题目 101 symmetric tree

https://leetcode.com/problems/symmetric-tree/

## 思路：
Recursion

iteration(BFS)

**需要构造辅助函数**
```
这类题目通常只用根节点子树对称性无法完全解决问题，必须要用到子树的某一部分进行递归，即要调用辅助函数比较两个部分子树。
形式上主函数参数列表只有一个根节点，辅助函数参数列表有两个节点
```


## 答案：101. Symmetric Tree
![c](https://github.com/SSRRBB/Leetcode/blob/main/Images/260.png)
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
        ##if left == None or right == None or left.val != right.val:
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

## 题目：100. Same Tree

https://leetcode.com/problems/same-tree/


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
        if queue1 or queue1:
            return False
        return True
 
```


## 题目：572. Subtree of Another Tree
Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

Example 1:
```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```
Example 2:
```
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
``` 
Constraints:
```
The number of nodes in the root tree is in the range [1, 2000].
The number of nodes in the subRoot tree is in the range [1, 1000].
-104 <= root.val <= 104
-104 <= subRoot.val <= 104
```

## 思路：
分治法；
两层递归
```
#  特殊判断：都为空成立；有一颗树为空就不成立
# 先判断两棵树是否是相同，如果相同那么就是满足题意的(100 same subtree)
# 然后判断一棵树的左子树是否是另一颗树的子树/一棵树的右子树是否是另一颗树的子树
```

![c](https://github.com/SSRRBB/Leetcode/blob/main/Images/109.png)


## 答案：
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        # 非空树不是空树的子树
        if root is None and subRoot: 
            return False
        # 空数是非空树的子树
        if root and subRoot is None:
            return True
        # 如果两棵树相等，是子树关系
        if self.isEqual(root, subRoot):
            return True
        
        # 如果T2是T1的左子树或右子树的子树，那么T2是T1的子树
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
        
        # return self.isSame(root, subRoot) or self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)

    def isEqual(self, root, subRoot):
        if root is None and subRoot is None:
            return True
        if root is None or subRoot is None:
            return False

        if root.val != subRoot.val:
            return False
        # 两棵树的左右子树相等，两棵树才相等    
        return self.isEqual(root.left, subRoot.left) and self.isEqual(root.right, subRoot.right)
        
```
