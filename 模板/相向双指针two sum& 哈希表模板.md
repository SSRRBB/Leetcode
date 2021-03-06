## 题目 1. Two sum
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]

## 思路：
方法一:
Hash table o(n), o(n)

方法二:
排序+相向双指针 o(nlogn)+o(n), 0(1)
```
思路[2, 4, 6, 9], target = 10

        #[2, 4, 6, 9]
        # ^        ^
        # L        R
   
        #numbers[L] + numbers[R] ? target
        #2 + 9 = 11 > 10, R--  L =0, R= 3
        #2 + 6 = 8 < 10. L++ L =0 , R =2
        #4 + 6 = 10. 完事 L =1, R =2
        #if 2,5,6,8 5+6 > 10.  R--则LR重合，不可以
```
        
## 预热答案（返回值，而非下标）(两个放法都不错)
### 法一 hash table
``` python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashset = set()
        for num in nums:
            if target - num in hashset:
                return num, target-num
            hashset.add(num) #放在if后面 防止[2， 4， 5], target 8
```
### 法二 sort + 相向双指针
``` Python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        #此方法o(nlogn), 0(1)
        numbers.sort() #o(nlogn)
        left, right = 0， len(numbers) - 1 # o(n)
        while left < right:
            if numbers[left] + number[right] > target:
                right -= 1
            elif numbers[left] + numbers[right] < target:
                left += 1
            else:
                return numbers[left], numbers[right]
```
## 答案（哈希表更好啊）
### 法一 hash table
``` python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
    
        #此方法o(n), 0(n)
        hash = {} #空字典
        for i, num in enumerate(nums):
            if target - num in hash: #在hash表上用key去找，所以有了hash[num] = i
                return[hash[target - num], i]
            hash[num] = i #num是hash表的key,i是hash表的value、下标
        #无解时：
        retun[-1, -1]           
```
### 法二 sort + 相向双指针
``` Python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        #此方法o(nlogn), 0(1)
        
        numbers = [
            (num, i)
            for i, num in enumerate(nums)
        ] #二元list
        
        numbers.sort()  #按照num的大小从小排到大 o(nlogn)
        
        left, right = 0, len(nums) - 1 #(o(n))
        while left < right:
            if numbers[left][0] + numbers[right][0] > target:
                right -= 1
            elif numbers[left][0] + numbers[right][0] < target:
                left += 1  
            else:
                return numbers[left][1], numbers[right][1]   
                #return sorted([nums[left][1], nums[right][1]]) # sorted是因为最后返回的下标要求他必须从小到大
        return [-1, -1]
 ```
# 相向双指针two sum 模板 sorted
## 题目 167. Two Sum II - Input Array Is Sorted
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

 
Example 1:
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```
Example 2:
```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].
```
Example 3:
```
Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].    
```
## 思路
方法一：排序+相向双指针 o(nlogn)+o(n), 0(1)

方法二：Hash table o(n), o(n)
```
思路[2, 4, 6, 9], target = 10
        #[2, 4, 6, 9]
        # ^        ^
        # L        R
        #numbers[L] + numbers[R] ? target
        #2 + 9 = 11 > 10, R--  L =0, R= 3
        #2 + 6 = 8 < 10. L++ L =0 , R =2
        #4 + 6 = 10. 完事 L =1, R =2
        
        #if 2,5,6,8 5+6 > 10.  R--则LR重合，不可以
 ```
## 答案（相向双指针two sum模板 sorted）
### 方法一：相向双指针 o(n), 0(1)
```Python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
##此方法0(n), 0(1)        
        left, right = 0, len(numbers) - 1
        while left < right:
            if numbers[left] + numbers[right] > target:
                right -= 1
            elif numbers[left] + numbers[right] < target:
                left += 1
            else:
                return left + 1, right + 1#注意审题
            
        return [-1, -1]

```
### 方法二：hash table o(n), 0(n)
```python       
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:        
        hash = {} #空字典
        for i, num in enumerate(numbers):
            if target - num in hash: #在hash表上用key去找，所以有了hash[num] = i
                return[hash[target - num] + 1, i + 1] # #注意审题
            hash[num] = i #num是hash表的key,i是hash表的value、下标
        #无解时：
        retun[-1, -1]
  ```
