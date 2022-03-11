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
       

**如果只让遍历一遍**
则要加上datastream lintcode 960 (1429 leetcode)
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

**只遍历一次**
```python
class Solution:
    """
    @param nums: a continuous stream of numbers
    @param number: a number
    @return: returns the first unique number
    """
    def firstUniqueNumber(self, nums, number):
     # Write your code here
        # 如果只遍历一次
        ds = DataStream()
        for i in range(len(nums)):
            ds.add(nums[i])
            if nums[i] == number: 
                   return ds.firstUnique()   
        return -1
## 960题目
class DataStream:

    def __init__(self):
        # do intialization if necessary
        #定义双链表，头尾都为dummy
        self.head = DlistNode()
        self.tail = DlistNode()
        #将头尾连起来
        self.head.next = self.tail
        self.tail.prev = self.head
        #存储链表DlistNode(节点)
        self.counter = dict()
        #存储出现过>=2次的数字
        self.duplicate = set()  
    """
    @return: the first unique number in stream
    """
    def firstUnique(self):
        # write your code here
        # first unique 在链表首部
        # 链表为空，返回-1
        if not self.head.next.next:
            return -1
        return self.head.next.value
           
    """
    @param num: next number in stream
    @return: nothing
    """
    def add(self, num):
        # write your code here
        # num第一次出现，加入链表尾部并加入哈希字典counter
        # num第二次出现，从链表中删除（利用哈希字典counter，o(1)找到其位置)并从conter中删除，再加入duplicatesetse
        # num第三、四次等出现，从直接忽略
        # 总结：链表和counter里面其实只有出现过一次的数据

        # 如果这个num出现过两次以上，立刻返回
        if num in self.duplicate:
            return

        # 如果这个num第一次出现
        if num not in self.counter:
            self.add_to_tail(num)
            return
        
        # 如果这个num第二次出现
        self.remove(num)

    def add_to_tail(self, num):
        node = DlistNode(num)
        node.prev = self.tail.prev
        node.next = self.tail
        #node.prev.next = node 
        self.tail.prev.next = node
        self.tail.prev = node
        self.counter[num] = node 

    def remove(self, num):
        if num in self.counter:
            node = self.counter[num]
            node.prev.next = node.next
            node.next.prev = node.prev
            del self.counter[num]
            self.duplicate.add(num)
            return


## 定义双链表
class DlistNode:
    def __init__(self, value = None):
        self.value = value
        self.prev = None 
        self.next = None




```
