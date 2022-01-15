## 题目：
Given a continuous stream of data, write a function that returns the first unique number (including the last number) when the terminating number arrives. If the terminating number is not found, return -1.

Example

Example1
```
Input: 
[1, 2, 2, 1, 3, 4, 4, 5, 6]
5
Output: 3
```
Example2
```
Input: 
[1, 2, 2, 1, 3, 4, 4, 5, 6]
7
Output: -1
```
Example3
```
Input: 
[1, 2, 2, 1, 3, 4]
3
Output: 3
```

![s](https://github.com/SSRRBB/Leetcode/blob/main/Images/151.png)


## 思路：
**时间和空间复杂度均为 o(n)
**hash 分类计数功能**

**dict.get(key, default=None)

**key -- 字典中要查找的键。

**default -- 如果指定键的值不存在时，返回该默认值。

![s](https://github.com/SSRRBB/Leetcode/blob/main/Images/152.png)
       

## 答案：
```python
class Solution:
    """
    @param nums: a continuous stream of numbers
    @param number: a number
    @return: returns the first unique number
    """
    def firstUniqueNumber(self, nums, number):
        # Write your code here
        if not nums:
            return -1
        #key:num    value:num出现次数
        counter = dict()
        for num in nums:
            #如果num还没有出现在counter中，默认次数0
            counter[num] = counter.get(num, 0) + 1
            if num == number:
                break
        #没有break, return -1
        else:
            return -1
        #再次遍历
        for num in nums:
            #遇到uqnique数字，立马返回
            if counter[num] == 1:
                return num

    

```
