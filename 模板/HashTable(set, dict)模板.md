set: https://www.runoob.com/python3/python3-set.html

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/276.png)


- **collections**
```
## This module implements specialized container datatypes providing alternatives 
# to Python’s general purpose built-in containers, dict, list, set, and tuple.

## Counter: dict subclass for counting hashable objects
## defaultdict:dict subclass that calls a factory function to supply missing values

OrderedDict dict subclass that remembers the order entries were added
deque list-like container with fast appends and pops on either end


```
- **dict.get(num, 0):如果num不存在，返回0； 存在则不管**
# dict.get(key, deafult = None)如果key不存在，返回None或者设置的值； 存在则不管

# collections.

```python
## 计数器一
dict = {}
for num in nums:
    dict[num] = dict.get(num, 0) + 1
    
## 计数器二
counter = collections.Counter(nums)

```

dict: https://www.runoob.com/python3/python3-dictionary.html
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/275.png)


## 题目：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/204.png)

## 思路：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/205.png)

## 答案：
```python
class MyQueue:
    def __init__(self):
        self.before_head = ListNode(-1) # dummy
        self.tail = self.before_head #dummy
    
    """
    @param: item: An integer
    @return: nothing
    """
    def enqueue(self, item):
        # write your code here
        # 把新node插入后面
        self.tail.next = ListNode(item)
        #后移tail指针
        self.tail = self.tail.next
    
    
    """
    @return: An integer
    """
    def dequeue(self):
        # write your code here
        #如果queue为空
        if self.before_head.next is None:
            return -1
        #记录队头数值
        head_val = self.before_head.next.val
        #后移before_head 指针
        self.before_head = self.before_head.next

        return head_val

class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None


```
