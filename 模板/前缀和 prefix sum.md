## 前缀和 （prefix sum）


- **这种通过记录数组前一部分的元素值来解题的思路，称为前缀和**
- **如果nums原数组中均为0或者正整数，那么前缀和是一个递增的序列**
- **哈希表中加入{0(pre) ：？}key(pre): value**

### 方法一(前面加哨兵)

**哈希表中加入{0(pre) ：？}key(pre): value**

**pre[i] = nums[i - 1] + pre[i - 1]**

**nums[i]到nums[j]直接的和：= pre[j+1] - pre[i]**
```
对于一个数组 nums,对应的前缀和pre
pre[0] = 0
pre[1] = nums[0] 

pre[i] = nums[0] + nums[1] + …… + nums[i - 1]

```
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/306.png)
**code**
```python
**求 pre[i] = nums[0] + nums[1] + …… + nums[i - 1]**

nums = [3, 5, 2, -2, 4, 1]
pre = [0] * (len(nums) + 1)
for i in range(1, len(nums) + 1):
    pre[i] = nums[i - 1] + pre[i - 1]
```

```python
**查看 nums[i] + …… + nums[j]**
def query(pre, i, j):
    return pre[j + 1] - pre[i]
```    


### 方法二(i = 0 时比较麻烦)

**哈希表中加入{0(pre) ：？}key(pre): value**

**pre[i] = nums[i] + pre[i - 1]**

**nums[i]到nums[j]直接的和：= pre[j] - pre[i - 1]**

```
对于一个数组 nums,对应的前缀和pre
pre[0] = nums[0]
pre[1] = nums[0] + nums[1]

pre[i] = nums[0] + nums[1] + …… + nums[i]
```
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/307.png)
**code**
```python
**求 pre[i] = nums[0] + nums[1] + …… + nums[i]**

nums = [3, 5, 2, -2, 4, 1]
pre = [0 for i in range(len(nums)]
for i in range(len(nums)):
    if i == 0:
        pre[i] = nums[i]
    else:
        pre[i] = nums[i] + pre[i - 1]
```

```python
**查看 nums[i] + …… + nums[j]**
def query(pre, i, j):
    if i == 0:
        return pre[j]
    else:
        return pre[j] - pre[i-1] 
```

# 题
## 1480. Running Sum of 1d Array
https://leetcode.com/problems/running-sum-of-1d-array/

就是上面写的思路
## 答案：
```python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
               
        pre = [0]* (len(nums) + 1)
     
        for i in range(1, len(nums) + 1):
            pre[i] = pre[i - 1] + nums[i - 1]
            
        return pre[1:]
        ########
        runningSum = [0]* len(nums)
        
        for i in range(len(nums)):
            if i == 0:
                runningSum[i] = nums[i]
            else:
                runningSum[i]=  runningSum[i - 1] + nums[i]
                
        return runningSum
```
## 303
https://leetcode.com/problems/range-sum-query-immutable/

就是上面写的思路

## 答案：
```python
class NumArray:
    def __init__(self, nums: List[int]):
        self.nums = nums
        self.pre = [0] * (len(self.nums) + 1)
        for i in range(1, len(self.nums) + 1):
            self.pre[i] = self.pre[i-1] + self.nums[i-1]
            
        #####
        self.nums = nums
        self.pre = [0] * len(self.nums)
        for i in range(len(self.nums)):
            if i == 0:
                self.pre[i] = self.nums[i]
            else:
                self.pre[i] = self.pre[i - 1] + self.nums[i]

    def sumRange(self, left: int, right: int) -> int:
        return self.pre[right + 1] - self.pre[left]
        
        #####
        if left == 0:
            return self.pre[right]
        return self.pre[right] - self.pre[left - 1]
        
# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```

## 304. Range Sum Query 2D - Immutable

https://leetcode.com/problems/range-sum-query-2d-immutable/

## 思路：
用加0的方法

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/309.png)

## 答案：
```python
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        n = len(matrix)
        m = len(matrix[0])
        
        self.pre = [[0] * (m + 1) for i in range(n + 1)]
        for i in range(1, n + 1):
            for j in range(1, m + 1):
                self.pre[i][j] = self.pre[i-1][j] + self.pre[i][j-1] + matrix[i -1][j-1] - self.pre[i-1][j-1]
        

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        return self.pre[row2 + 1][col2 + 1] - self.pre[row1][col2 + 1] - self.pre[row2 + 1][col1] + self.pre[row1][col1]
 
        


# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```
