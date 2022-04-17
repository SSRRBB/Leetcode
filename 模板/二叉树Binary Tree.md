## 二叉树 BFS and DFS：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/330.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/253.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/328.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/329.png)


## 二叉树 种类 Balanced binary tree, Bianry search Tree and Red-Black tree：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/331.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/332.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/333.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/334.png)

## 二叉树解法

```python
分治是特殊的遍历
二叉树是天然的分治结构
二叉树的分治本质是做后序遍历;所以我们好多题其实是DFS后序遍历(从下到上)

```

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/335.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/336.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/337.png)


- 二叉搜索树(BST):左子树节点的值<根节点的值，右子树节点的值>=根节点的值
- 相等情况的点可能在右子树，也可能在左子树，需要跟面试官澄清
+ 中序遍历结果有序（不下降的顺序，有些临点可能相等）
- 如果二叉树的中序遍历不是不下降序列，则一定不是BST
- 如果二叉树的中序遍历是不下降，也未必是BST
+ BST的高度：最好O(n);最坏o(logN);用o(h)表示更合适
## code
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
