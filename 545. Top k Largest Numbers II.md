## 题目：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/219.png)


## 思路：
**top K 在线问题 **
**heapq**
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/220.png)


## 答案：
```python
class Solution:
    """
    @param: k: An integer
    """
    def __init__(self, k):
        # do intialization if necessary
        self.k = k
        self.heap = []

    """
    @param: num: Number to be added
    @return: nothing
    """
    def add(self, num):
        # write your code here
        # 最小堆中插入数据
        # 如果最小堆的长度大于K，则pop出最小值
        import heapq
        heapq.heappush(self.heap, num)
        if len(self.heap) > self.k:
            heapq.heappop(self.heap)

    """
    @return: Top k element
    """
    def topk(self):
        # write your code here
        #如果是heap.sort()则会生成新的heap
        return sorted(self.heap, reverse = True)


```


