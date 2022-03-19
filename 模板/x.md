## double Likelist
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/160.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/161.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/162.png)

```python
## 删除
def remove_node(self, node):
    node.prev.next = node.next
    node.next.prev = node.prev
    
## 插入
def add_to_tail(self, node):
    node.prev = self.tail.prev 
    node.next = self.tail 
    node.prev.next = node 
    #self.tail.prev.next = node
    self.tail.prev = node

## 定义双链表
class DlistNode:
    def __init__(self, key= None, value = None):
        self.key = key
        self.val = value
        self.prev = None
        self.next = None

```
