# *****二叉树 BFS and DFS：
```
BFS
DFS
```

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/330.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/253.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/328.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/329.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/338.png)

# *****二叉树 种类 Balanced binary tree, Bianry search Tree and Red-Black tree：
```
BST常考
```

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/331.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/332.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/333.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/334.png)

# *****二叉树解法

```python
分治是特殊的遍历
二叉树是天然的分治结构
二叉树的分治本质是做后序遍历;所以我们好多题其实是DFS后序遍历(从下到上)

```

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/335.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/336.png)
############################################################
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/337.png)

## *****code
```python
Class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
```

```python
Class TreeNode:
    def __init__(self, val):
        self.val = val
        self.children = None
