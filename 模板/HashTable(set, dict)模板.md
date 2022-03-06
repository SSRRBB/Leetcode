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
counter = collections.Couner()
for num in nums:
    counter[num] += 1

```

https://www.runoob.com/python3/python3-dictionary.html

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
