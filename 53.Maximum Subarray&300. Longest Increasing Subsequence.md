## 题目：53. Maximum Subarray

https://leetcode.com/problems/maximum-subarray/

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
Example 2:
```
Input: nums = [1]
Output: 1
```
Example 3:
```
Input: nums = [5,4,-1,7,8]
Output: 23
``` 

Constraints:
```
1 <= nums.length <= 105
-104 <= nums[i] <= 104
```

## 答案：
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        if not nums:
            return 0
        dp = [0 for _ in range(len(nums))] ##1. 确定dp数组(dp table)以及下标的含义！！！！！：表示以 nums[i] 结尾的连续子数组的最大和。
        dp[0] = nums[0] ## 3.dp数组如何初始化
        for i in range(1, len(nums)):  #2&4确定递推公式;遍历顺服
            if dp[i - 1] >= 0:
                dp[i] = dp[i - 1] + nums[i]
            else:
                dp[i] = nums[i]
        return max(dp)
```

```python
################(把递推公式合起来写)
        if not nums:
            return 0

        dp = [0 for _ in range(len(nums))]
        dp[0] = nums[0]
        res = dp[0]
        for i in range(1, len(nums)):
            dp[i] = max(dp[i - 1] + nums[i], nums[i])   # 更新dp[i]
            res = max(res, dp[i])  # 更新全局最大值
        return res
```

## 思路：

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/430.png)

## 题目：300. Longest Increasing Subsequence

https://leetcode.com/problems/longest-increasing-subsequence/

Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

 

Example 1:
```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```
Example 2:
```
Input: nums = [0,1,0,3,2,3]
Output: 4
```
Example 3:
```
Input: nums = [7,7,7,7,7,7,7]
Output: 1
```

Constraints:
```
1 <= nums.length <= 2500
-104 <= nums[i] <= 104
 
```
Follow up: Can you come up with an algorithm that runs in O(n log(n)) time complexity?

## 思路：
https://leetcode.cn/problems/longest-increasing-subsequence/solution/chuan-shang-yi-fu-wo-jiu-bu-ren-shi-ni-liao-lai-li/

**follow up:**

https://leetcode.cn/problems/longest-increasing-subsequence/solution/dong-tai-gui-hua-er-fen-cha-zhao-tan-xin-suan-fa-p/
## 答案：
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        #### 时间O(n^2)
        n = len(nums)
        if n == 0: 
            return 0
        dp = [1] * n ##以 nums[i] 结尾 的「上升子序列」的长度
        dp[0] = 1
        res = 1
        for i in range(1, n):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
                    res = max(res, dp[i])
        return  res
        
        n = len(nums)
        if n == 0: 
            return 0
        dp = [1] * n ##以 nums[i] 结尾 的「上升子序列」的长度
        dp[0] = 1
        for i in range(1, n):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
        return  max(dp)

```
**follow-up:**
```python

class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        size = len(nums)
        # 特判
        if size < 2:
            return size

        # 为了防止后序逻辑发生数组索引越界，先把第 1 个数放进去
        tail = [nums[0]]
        for i in range(1, size):
            # 【逻辑 1】比 tail 数组实际有效的末尾的那个元素还大
            # 先尝试是否可以接在末尾
            if nums[i] > tail[-1]:
                tail.append(nums[i])
                continue

            # 使用二分查找法，在有序数组 tail 中
            # 找到第 1 个大于等于 nums[i] 的元素，尝试让那个元素更小
            left = 0
            right = len(tail) - 1
            while left < right:
                # 选左中位数不是偶然，而是有原因的，原因请见 LeetCode 第 35 题题解
                # mid = left + (right - left) // 2
                mid = (left + right) >> 1
                if tail[mid] < nums[i]:
                    # 中位数肯定不是要找的数，把它写在分支的前面
                    left = mid + 1
                else:
                    right = mid
            # 走到这里是因为【逻辑 1】的反面，因此一定能找到第 1 个大于等于 nums[i] 的元素，因此无需再单独判断
            tail[left] = nums[i]
        return len(tail)
```

**思路**
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/431.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/432.png)
