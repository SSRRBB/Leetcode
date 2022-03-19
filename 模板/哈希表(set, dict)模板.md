# Set: 
https://www.runoob.com/python3/python3-set.html

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/276.png)

# Dict

- **collections**

https://docs.python.org/zh-cn/3.8/library/collections.html

https://docs.python.org/3/library/collections.html
```
##This module implements specialized container datatypes providing alternatives 
# to Python’s general purpose built-in containers, dict, list, set, and tuple.
```

- **Counter**: dict subclass for counting hashable objects 
**返回key : val /// val只是int**
```
c = collections.Counter()                          # a new, empty counter
c = collections.Counter('gallahad')                 # a new counter from an iterable
print(c)  Counter({'a': 3, 'l': 2, 'g': 1, 'h': 1, 'd': 1})
c = collections.Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
print(c)  Counter({'red': 4, 'blue': 2})
c = collections.Counter(cats=4, dogs=8)  Counter({'dogs': 8, 'cats': 4})

```
- **defaultdict**:dict subclass that calls a factory function to supply missing values
**返回key : val ///  val是list, set**
```
# Using list as the default_factory, it is easy to group a sequence of key-value pairs into a dictionary of lists:

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = collections.defaultdict(list)
for k, v in s:
    d[k].append(v)
print(d)  defaultdict(<class 'list'>, {'yellow': [1, 3], 'blue': [2, 4], 'red': [1]})

# Setting the default_factory to set makes the defaultdict useful for building a dictionary of sets:
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = collections.defaultdict(set)
for k, v in s:
    d[k].add(v)
print(d) defaultdict(<class 'set'>, {'yellow': {1, 3}, 'blue': {2, 4}, 'red': {1}})

```
- **OrderedDict**:dict subclass that remembers the order entries were added
- 
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/167.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/168.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/169.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/170.png)

- **deque**: list-like container with fast appends and pops on either end



- **dict.get(num, 0)**
```
dict.get(num, 0):如果num不存在，返回0； 存在则不管

dict.get(key, deafult = None): 如果key不存在，返回None或者设置的值； 存在则不管

```
## 计数器
```python
## 计数器一
dict = {}
for num in nums:
    dict[num] = dict.get(num, 0) + 1
    
## 计数器二
counter = collections.Counter(nums)

or 
counter = collections.Counter()
for num in nums:
    counter[num] += 1

```
## val is list or set
```python

d = collections.defaultdict(list)
for k, v in s:
    d[k].append(v)

d = collections.defaultdict(set)
for k, v in s:
    d[k].add(v)

```

https://www.runoob.com/python3/python3-dictionary.html

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/275.png)


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

        
## 预热答案（返回值，而非下标）(两个放法都不错)
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
## 题目: 454.4sum II
https://leetcode.com/problems/4sum-ii/solution/
## 思路：
## 思路
**哈希表（折半查询法）**
```
This problem is a variation of 4Sum, and we recommend checking that problem first.
The main difference is that here we pick each element from a different array, 
while in 4Sum all elements come from the same array. 
For that reason, we cannot use the Two Pointers approach, where elements must be in the same sorted array.
```
## 答案：
```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        # key 为 a+b之和，value为出现频率
        counter = {}
        
        for num1 in nums1:
            for num2 in nums2:
                total = num1 + num2 
                #如果counter里面没有 total,返回默认频率0
                counter[total] = counter.get(total, 0) + 1
                #if total in counter:
                    #counter[total] += 1
                #else:
                    #counter[total] = 1

        cnt = 0  
        for num3 in nums3:
            for num4 in nums4:
                total = num3 + num4 
                #如果-total出现在counter里面，累加频率，否则默认频率0
                #cnt += counter.get(-total, 0)
                if -total in counter:
                    cnt += counter[-total]
        return cnt
```
