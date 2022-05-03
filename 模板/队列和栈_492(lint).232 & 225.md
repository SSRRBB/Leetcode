![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/270.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/271.png)

## 题目：232. Implement Queue using Stacks
https://leetcode.com/problems/implement-queue-using-stacks/solution/
## 思路：
```
push: O(1),O(n)
empty: O(1), O(1)
peek similar with pop

pop:
Time complexity: Amortized O(1),  Worst-case O(n).
Space complexity: O(1).

In the worst-case scenario when stack b is empty, 
the algorithm pops n elements from stack a and pushes n elements to s2, where n is the queue size.
This gives 2n operations, which is O(n). 
But when stack s2 is not empty the algorithm has O(1) time complexity. 
So what does it mean by Amortized O(1)? Please see the next section on Amortized Analysis for more information.


Amortized Analysis
The amortized analysis gives the average performance (over time) of each operation in the worst case. 
The basic idea is that a worst-case operation can alter the state 
in such a way that the worst case cannot occur again for a long time, thus amortizing its cost.
```
## 答案：
```python
class MyQueue:

    def __init__(self):
        self.a = []
        self.b = []

    def push(self, x: int) -> None:
        self.a.append(x)

    def pop(self) -> int:
        # 如果栈b不为空，直接pop即可
        if self.b:
            return self.b.pop()
        # 如果栈b为空，需要先将栈a中的数据倒腾到栈b中，再pop
        while self.a:
            self.b.append(self.a.pop())
        return self.b.pop()

    def peek(self) -> int:
        # 如果栈b不为空，直接peek即可
        if self.b:
            return self.b[-1]
        # 如果栈b为空，需要先将栈a中的数据倒腾到栈b中，再peek    
        while self.a:
            self.b.append(self.a.pop())
        return self.b[-1]

    def empty(self) -> bool:
        # 栈a和栈b需要同时判空
        return len(self.a) == 0 and len(self.b) == 0
        


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()

```

## 题目：225. Implement Stack using Queues
https://leetcode.com/problems/implement-stack-using-queues/

## 思路：
```
push
使用一个队列时，为了满足栈的特性，即最后入栈的元素最先出栈，同样需要满足队列前端的元素是最后入栈的元素。

入栈操作时，首先获得入栈前的元素个数 n，然后将元素入队到队列，
再将队列中的前 n个元素（即除了新入栈的元素之外的全部元素）依次出队并入队到队列，
此时队列的前端的元素即为新入栈的元素，且队列的前端和后端分别对应栈顶和栈底。

时间复杂度：push为O(n),其他为O(1)
The algorithm removes n elements and inserts n+1 elements to q1 , 
where n is the stack size. This gives 2n+1 operations. 
空间复杂度：都为O(1)
```

## 答案
```python
class MyStack:

    def __init__(self):
        self.queue = collections.deque()

    def push(self, x: int) -> None:
        n = len(self.queue)
        self.queue.append(x)
        for _ in range(n):
            self.queue.append(self.queue.popleft())

    def pop(self) -> int:
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[0]

    def empty(self) -> bool:
        return not self.queue
        


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()

```
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
