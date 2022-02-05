## 题目 144(lint) Interleaving Positive and Negative Numbers

Given an array with positive and negative integers. Re-range it to interleaving with positive and negative integers.
You are not necessary to keep the original order of positive integers or negative integers.

Example
```
Example 1
Input : [-1, -2, -3, 4, 5, 6]
Outout : [-1, 5, -2, 4, -3, 6]
Explanation :  any other reasonable answer.
Challenge
Do it in-place and without extra memory.
```
## 思路
partition 模板 升级
![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/19.png)

![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/20.png)

![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/21.png)

![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/22.png)
## 答案
```python
class Solution:
    """
    @param: A: An integer array.
    @return: nothing
    """
    def rerange(self, A):
        # write your code here
        neg_cnt = self.partition(A)
        pos_cnt = len(A) - neg_cnt
        #根据真负数个数的情况设定left，right
        left = 1 if neg_cnt > pos_cnt else 0
        right = len(A) -  (2 if neg_cnt < pos_cnt else 1)
        
        self.interleave(A, left, right)
    
    #左分区为负数，右分区为正数
    def partition(self, A):
        left, right = 0, len(A) - 1
        while left <= right:
            while left <= right and A[left] < 0:
                left += 1
            while left <= right and A[right] > 0:
                right -= 1
            if left <= right:
                A[left], A[right] = A[right], A[left]
                left += 1
                right -= 1
        return left #这行让我们知道复数的个数[start, right]&[left, end]
    
    #两端对调，实现正负交替
    def interleave(self, A, left, right):
        while left < right:
            A[left], A[right] = A[right], A[left]
            left, right = left + 2, right - 2 #是2，间隔交换
```

## 题目 922. Sort Array By Parity II
Given an array of integers nums, half of the integers in nums are odd, and the other half are even.

Sort the array so that whenever nums[i] is odd, i is odd, and whenever nums[i] is even, i is even.

Return any answer array that satisfies this condition.

 

Example 1:
```
Input: nums = [4,2,5,7]
Output: [4,5,2,7]
Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
```
Example 2:
```
Input: nums = [2,3]
Output: [2,3]
```
## 答案
```python
class Solution:
    def sortArrayByParityII(self, nums: List[int]) -> List[int]:
        self.partition(nums) 
        left, right = 0, len(nums) - 1
        self.interleave(nums, left, right)
        return nums
    
    def partition(self, nums): 
        left, right = 0, len(nums) - 1
        while left <= right:
            while left <= right and nums[left] % 2 == 1:
                left += 1
            while left <= right and nums[right] % 2 == 0:
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
                
    def interleave(self, nums, left, right):
        #left, right = 0, len(nums) - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left, right = left + 2, right - 2
        
```
