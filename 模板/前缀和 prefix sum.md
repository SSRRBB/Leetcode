## 前缀和 （prefix sum）
https://leetcode-cn.com/problems/continuous-subarray-sum/solution/de-liao-wo-ba-qian-zhui-he-miao-de-gan-g-c8kp/

https://labuladong.github.io/algo/2/22/58/

- **这种通过记录数组前一部分的元素值来解题的思路，称为前缀和**
- **如果nums原数组中均为0或者正整数，那么前缀和是一个递增的序列**

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
## 思路：
就是上面写的
## 答案：
```python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        
        runningSum = [0]* len(nums)
        
        for i in range(len(nums)):
            if i == 0:
                runningSum[i] = nums[i]
            else:
                runningSum[i]=  runningSum[i - 1] + nums[i]
                
        return runningSum
        #####
        pre = [0]* (len(nums) + 1)
        
        for i in range(1, len(nums) + 1):
            pre[i] = pre[i - 1] + nums[i - 1]
            
        return pre[1:]
```



