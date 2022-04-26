## 题目：
https://leetcode.com/problems/subsets/




## 思路：
回溯(算法心得，负雪明烛)

正规写法

简单写法: 不需要copy.deepcopy()

时间复杂度：O(n* 2^n)

空间负责度：O(n)


## 答案：
### 78
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
     #for循环的意义是，从后序元素nums[index: n-1]中挑选元素
     ##正规写法
        res = []
        path = []
        self.dfs(nums, 0, res, path )
        return res
    
    def dfs(self, nums, index, res, path):
        if index > len(nums):
            return ##递归退出条件
        res.append(copy.deepcopy(path))#深度copy
        for i in range(index, len(nums)):
            path.append(nums[i])
            self.dfs(nums, i + 1, res, path)
           ## 回溯
            path.pop() ##递归几次(self.dfs几次)，就pop几次；然后执行下一个i
            
    ##简化写法
        res = []
        path = []
        self.dfs(nums, 0, res, path)
        return res
    def dfs(self, nums, index, res, path):
        if index > len(nums):
            return ##递归退出条件
        res.append(path) #每次都有新的path,不用深度copy
        for i in range(index, len(nums)):
            self.dfs(nums, i + 1, res, path + [nums[i]])
```
### 90
```python

```


