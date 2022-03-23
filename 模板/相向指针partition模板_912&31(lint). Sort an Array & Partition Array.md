## 题目：31(lint)Partition Array
Given an array nums of integers and an int k, partition the array (i.e move the elements in "nums") such that:

All elements < k are moved to the left
All elements >= k are moved to the right
Return the partitioning index, i.e the first index i nums[i] >= k.
Example 1:

Input:
nums = []
k = 9
Output:
0
Explanation:Empty array, print 0.

Example 2:
Input:
nums = [3,2,2,1]
k = 2
Output:
1
Explanation:the real array is[1,2,2,3].So return 1.

## 思路

**时间O(n), 空间O(1)**

**parition 相向双指针(来自quick sort 模板), 

**do it in place/no extra space/constan memory/o(1) space**

**partition类双指针算法模板:**

![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/18.png)
![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/17.png)

## 答案
``` Python
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        # write your code here
        left, right = 0, len(nums) - 1

        while left <= right:
            while left <= right and nums[left] < k:
                left += 1
            while left <= right and nums[right] >= k:#注意这一符号
                right -= 1
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        
        return left#注意返回值
```

## 题目 912.Sort an Array
Given an array of integers nums, sort the array in ascending order.

Example 1:
Input: nums = [5,2,3,1]
Output: [1,2,3,5]

Example 2:
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]

## 思路

**quick sort: 时间o(nlogn)-o(n2), 空间o(logn)-o(n) need additional space to store the recursive call stack.**

![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/30.png)
![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/31.png)
![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/32.png)

## 答案
```python
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        self.quickSort(nums, 0, len(nums) - 1)
        return nums
    
    # 递归三要素之一：递归的定义    
    def quickSort(self, nums, start, end):
        #递归三要素之三：递归的出口
        #如果start大于等于end,返回
        if start >= end:
            return
        
        #递归的三要素之二：递归的拆解
        #partition分区 
        left, right = start, end
        pivot = nums[(start + end) // 2]
        
        while left <= right: ##一定不要把这个符号搞错！！！
            while left <= right and nums[left] < pivot:
                left += 1
                
            while left <= right and nums[right] > pivot:
                right -= 1
            
            if left <= right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        
                        
        #递归        
        self.quickSort(nums, start, right)
        self.quickSort(nums, left, end)
 ```
 
## 题目: 912.Sort an Array
## 思路:
**merge sort: 时间O(nlogn), 空间O(n)**

![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/33.png)
![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/34.png)
![pre](https://github.com/SSRRBB/Leetcode/blob/main/Images/35.png)


## 答案
```python
class Solution:
    """
    @param A: an integer array
    @return: nothing
    """
    def sortIntegers2(self, A):
        # write your code here
        temp = [0] * len(nums)
        #tmp = [0 for _ in range(len(A))] #[4, 1, 3, 3, 5] [0, 0, 0, 0, 0]
        self.merge_sort(A, tmp, 0, len(A) - 1)

    # 递归三要素之一：递归的定义
    def merge_sort(self, A, tmp, start, end): #[start, end]
        #递归三要素之三：递归的出口 #如果start大于等于end,返回
        if start >= end:
            return
        #递归的三要素之二：递归的拆解
        mid = (start + end) //2 #[start, mid] [mid + 1, end]
        # divided，归并排序左边右边
        self.merge_sort(A, tmp, start, mid)
        self.merge_sort(A, tmp, mid + 1, end)
        # conquer,合并两边
        self.merge(A, tmp, start, mid, end) 

    def merge(self, A, tmp, start, mid, end):#核心思想
        left_index = start
        right_index = mid + 1
        index = start

        while left_index <= mid and right_index <= end:
            if A[left_index] <= A[right_index]:
                tmp[index] = A[left_index]
                index += 1
                left_index += 1
            else:
                tmp[index] = A[right_index]
                index += 1
                right_index +=1
        #不肯能两边同时剩下，只可能有一边剩下
        #处理左边剩下的
        while left_index <= mid:
            tmp[index] = A[left_index]
            index += 1
            left_index += 1
        #处理右边剩下的
        while right_index <= end:
            tmp[index] = A[right_index]
            index += 1
            right_index += 1
        #更新源数据
        for i in range(start, end + 1):
            A[i] = tmp[i]
 ```
