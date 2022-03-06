set: https://www.runoob.com/python3/python3-set.html

dict: https://www.runoob.com/python3/python3-dictionary.html

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/276.png)
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
