## 题目：580& 590. N-ary Tree Preoder &Postorder Traversal
https://leetcode.com/problems/n-ary-tree-preorder-traversal/

https://leetcode.com/problems/n-ary-tree-postorder-traversal/


## 思路：
DFS Recursion & iteration(常规)

## 答案
**preorder Recursion & iteration(常规)**
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def preorder(self, root: 'Node') -> List[int]:
        # recursion写法
        res = []
        
        def traverse(root):
            if not root:
                return
            res.append(root.val)
            for i in root.children:
                traverse(i)
        traverse(root)
        return res
       
        # iteration写法
        if not root:
            return []
        stack = [root]
        res = []
        while stack:
            node = stack.pop()
            res.append(node.val) # 根节点加入res
            if node.children:
                stack.extend(node.children[::-1])
    
        return res

   
        

```

**postorder Recursion & iteration(常规)**
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def postorder(self, root: 'Node') -> List[int]:
        # recursion 写法
        res = []
        
        def traverse(root):
            if not root:
                return
            for i in root.children:
                traverse(i)
            res.append(root.val)
        traverse(root)
        return res
            
        # iteration 写法
        if not root:
            return root
        
        res = []
        stack = [root]
        while stack:
            node = stack.pop()
            res.append(node.val)
            if node.children:
                stack.extend(node.children)
        return res[::-1]
        
        

```
