## 题目
Description
Given an array of integers, find how many pairs in the array such that their sum is less than or equal to a specific target number. Please return the number of pairs.

Example
Example 1:
```
Input: nums = [2, 7, 11, 15], target = 24. 
Output: 5. 
Explanation:
2 + 7 < 24
2 + 11 < 24
2 + 15 < 24
7 + 11 < 24
7 + 15 < 24
```

Example 2:
Input: nums = [1], target = 1. 
Output: 0. 

## 思路
** 双指针 **
two sum（基本框架+而且target是外面的，就不用for in range什么什么） + valid triangle number(用ant计数)

O(nlong) + O(n)
O(1)

## 答案
```python
class Solution:
    """
    @param nums: an array of integer
    @param target: an integer
    @return: an integer
    """
    def twoSum5(self, nums, target):
        # write your code here
        if not nums or len(nums) < 2 :
            return 0
        
        nums.sort()

        ans = 0
        left, right = 0, len(nums) - 1
        while left < right:
            two_sum = nums[left] + nums[right]
            if  two_sum <= target:
                ans += right - left
                left += 1
            else:
                right -= 1
                
        
        return ans
```
