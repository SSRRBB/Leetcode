## 题目：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/194.png)

## 思路：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/195.png)


## 答案：
```python
"""
Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    """
    @param head: The head of linked list.
    @param val: An integer.
    @return: The head of new linked list.
    """
    def insertNode(self, head, val):
        # write your code here
        #创建dummy node
        dummy = ListNode(float('-inf'))
        dummy.next = head
        curr_Node = dummy
        while curr_Node.next and curr_Node.next.val <= val:
            curr_Node = curr_Node.next
        #插入新节点
        new_node = ListNode(val)
        new_node.next = curr_Node.next
        curr_Node.next = new_node
        #插入新节点方法二
        new_node = ListNode(val)
        curr_Node_next = curr_Node.next
        curr_Node.next = new_node
        new_node.next = curr_Node_next
    
    
        return dummy.next


```
