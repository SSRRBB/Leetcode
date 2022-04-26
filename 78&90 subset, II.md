## 题目：
https://leetcode.com/problems/subsets/

https://leetcode.com/problems/subsets-ii/


## 思路：
回溯(算法心得，负雪明烛)

1. 正规写法 :正规写法对应了**全局共享一个 path 的写法，每次添加到 res 中，需要深度拷贝。python中是需要 copy.deepcopy(path) **

C++ 的 vector 的 push_back() 函数，本身就是深度拷贝。另外由于是全局的 path，因此每次需要对 path 进行 push 和 pop 操作，

2. 简单写法: **每次新建 path，使用的是产生一个新数组 path + [s[:i]]**. 这样好处是方便：不同的路径使用的是不同的 path，**a.因此不需要 path.pop() 操作；b. 而且 res.append(path) 的时候不用深度拷贝一遍 path。**

时间复杂度：O(n* 2^n)

空间复杂度：O(n)

```
回溯法
一般情况下，看到题目要求「所有可能的结果」，而不是「结果的个数」，我们就知道需要暴力搜索所有的可行解了，可以用「回溯法」。
「回溯法」实际上一个类似枚举的搜索尝试过程，主要是在搜索尝试过程中寻找问题的解，当发现已不满足求解条件时，就「回溯」返回，尝试别的路径。
回溯法是一种算法思想，而递归是一种编程方法，回溯法可以用递归来实现。
```
*****
90
```
如果你能理解上面的回溯法，那么包含重复元素的数组的子集，只不过一个小的改进。
比如说求 nums = [1,2,2] 的子集，那么对于子集 [1,2] 是选择了第一个 2，那么就不能再选第二个 2 来构成 [1,2] 了。

所以，此时的改动点，就是先排序，
每个元素 nums[i] 添加到 path 之前，判断一下 nums[i] 是否等于 nums[i - 1] ，如果相等就不添加到 path 中
```

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
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        res = []
        path = []
        nums.sort()
        self.dfs(nums, 0, res, path)
        return res
    
    def dfs(self, nums, index, res, path):
        res.append(copy.deepcopy(path))
        for i in range(index, len(nums)):
            if i > index and nums[i] == nums[i -1]: #i>index意思就是不用判断nums[0]和nums[-1]
                continue
            path.append(nums[i])
            self.dfs(nums, i + 1, res, path)
            path.pop()
            
        ##简单
        res = []
        path = []
        nums.sort()
        self.dfs(nums, 0, res, path)
        return res
    
    def dfs(self, nums, index, res, path):
        res.append(path)
        for i in range(index, len(nums)):
            if i > index and nums[i] == nums[i - 1]:
                continue
            self.dfs(nums, i + 1, res, path + [nums[i]] )
 
```


