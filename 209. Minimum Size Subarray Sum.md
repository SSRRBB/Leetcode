## 题目：
Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

 

Example 1:
```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```
Example 2:
```
Input: target = 4, nums = [1,4,4]
Output: 1
```
Example 3:
```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```
 

Constraints:
```
1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 105
```

## 思路：
**同向双指针 sliding window**

**滑动窗口的精髓就是动态调节滑动窗口的起始位置：根据子序列之和**
```
while curr_sum >= target:
    res = min(res, end - start + 1 )
    curr_sum -= nums[start]
    start += 1
```
**滑动窗口三要素**
### 窗口内是什么?curr_sum
### 如何移动窗口的起始位置start？start = 0:根据子序列之和动态调节start位置
### 如何移动窗口的终止位置end？ for end in range(len(nums))
时间复杂度：O(n)，其中 n 是数组的长度。指针 start 和 end 最多各移动 n 次。
空间复杂度：O(1)。

**来自其他人**
### 可变窗口大小

对于可变窗口，我们同样固定初始化左右指针 l 和 r，分别表示的窗口的左右顶点。后面有所不同，我们需要保证：

1. l 和 r 都初始化为 0
2. r 指针移动一步
3. 判断窗口内的连续元素是否满足题目限定的条件
   - 3.1 如果满足，再判断是否需要更新最优解，如果需要则更新最优解。并尝试通过移动 l 指针缩小窗口大小。循环执行 3.1
   - 3.2 如果不满足，则继续。

形象地来看的话，就是 r 指针不停向右移动，l 指针仅仅在窗口满足条件之后才会移动，起到窗口收缩的效果。

![](https://tva1.sinaimg.cn/large/007S8ZIlly1ghlugl94y8j30d90d50t5.jpg)

### 伪代码

```
初始化慢指针 = 0
初始化 ans

for 快指针 in 可迭代集合
   更新窗口内信息
   while 窗口内不符合题意
      扩展或者收缩窗口
      慢指针移动
   更新答案
返回 ans
```


## 答案：
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        ##同向双指针sliding window
        res = len(nums) + 1 #float('inf')
        start = 0 
        curr_sum = 0
        for end in range(len(nums)):
            curr_sum += nums[end]
            while curr_sum >= target:
                res = min(res, end - start + 1 )
                curr_sum -= nums[start]
                start += 1
                
        return 0 if res == len(nums) + 1 else res



```
