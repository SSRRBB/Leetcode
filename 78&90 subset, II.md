## 题目：
https://leetcode.com/problems/subsets/

https://leetcode.com/problems/subsets-ii/


## 思路：
```
子集或者组合；回溯;DFS

时间复杂度：O(n* 2^n)

空间复杂度：O(n)
```





**90同层之间不能重复元素，类似40**
```
如果你能理解上面的回溯法，那么包含重复元素的数组的子集，只不过一个小的改进。
比如说求 nums = [1,2,2] 的子集，那么对于子集 [1,2] 是选择了第一个 2，那么就不能再选第二个 2 来构成 [1,2] 了。

此时的改动点     1. 就是先排序，
               2.每个元素 nums[i] 添加到 path 之前，判断一下 nums[i] 是否等于 nums[i - 1] ，如果相等就不添加到 path 中
```

## 答案：
### 78
```python
#for循环的意义是，从后序元素nums[index: n-1]中挑选元素
     ##简化写法
        res = []
        path = []
        self.dfs(nums, 0, res, path)
        return res
    
    def dfs(self, nums, index, res, path):
        if index > len(nums):
            return ##递归出口
        res.append(path) #每次都有新的path,不用深度copy
        for i in range(index, len(nums)):  #for就要从startIndex开始，而不是从0开始！
            self.dfs(nums, i + 1, res, path + [nums[i]])

        
     ##正规写法
        res = []
        path = []
        self.dfs(nums, 0, res, path )
        return res
    
    def dfs(self, nums, index, res, path):
        if index > len(nums):
            return ##递归出口
        res.append(copy.deepcopy(path))#深度copy
        for i in range(index, len(nums)):
            path.append(nums[i])
            self.dfs(nums, i + 1, res, path)
           ## 回溯
            path.pop() ##递归几次(self.dfs几次)，就pop几次；然后执行下一个i
```
### 90
```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
                    
        ##简单
        res = []
        path = []
        nums.sort()
        self.dfs(nums, 0, res, path)
        return res
    
    def dfs(self, nums, index, res, path):
        if index > len(nums):
            return #递归出口
        res.append(path)
        for i in range(index, len(nums)):
            if i > index and nums[i] == nums[i - 1]:#i>index意思就是不用判断nums[0]和nums[-1]
                continue #不能选重复的数递归
            self.dfs(nums, i + 1, res, path + [nums[i]])
            
            ####正规
        res = []
        path = []
        nums.sort()
        self.dfs(nums, 0, res, path)
        return res
    
    def dfs(self, nums, index, res, path):
        if index > len(nums):
            return #递归出口
        res.append(copy.deepcopy(path))
        for i in range(index, len(nums)):
            if i > index and nums[i] == nums[i -1]: #i>index意思就是不用判断nums[0]和nums[-1]
                continue
            path.append(nums[i])
            self.dfs(nums, i + 1, res, path)
            path.pop()     

```
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/368.png)
**90**
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/404.png)


