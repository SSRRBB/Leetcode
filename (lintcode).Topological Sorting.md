## 题目：127(lintcode).Topological Sorting.md
![p](https://github.com/SSRRBB/Leetcode/blob/main/Images/88.png)


## 思路:
详细可参考 210. Course Schedule II
BFS-求任意拓扑排序

![p](https://github.com/SSRRBB/Leetcode/blob/main/Images/89.png)

## 答案：
```python

"""
class DirectedGraphNode:
     def __init__(self, x):
         self.label = x
         self.neighbors = []
"""

class Solution:
    """
    @param graph: A list of Directed graph node
    @return: Any topological order for the given graph.
    """
    def topSort(self, graph):
        # write your code here
         #1. 统计每个点的入度 
        node_to_indegree = self.get_indegree(graph)
        
        #2.讲每个入度为0的点放入queue
        # bfs
        order = [] #记录拓扑顺序
        start_nodes = [n for n in graph if node_to_indegree[n] == 0]
        queue = collections.deque(start_nodes)
        #3.不断从队列中拿出一个点，去掉这个点的所有连边（指向其他店的边）
        #其他点的相应入度为 -1
        while queue:
            node = queue.popleft()
            order.append(node)
            for neighbor in node.neighbors:
                node_to_indegree[neighbor] -= 1
                # 4. 当前点的所有邻居入度减1，如果入度降为 0，再加入队列
                if node_to_indegree[neighbor] == 0:
                    queue.append(neighbor)
                
        return order
    
    # 统计每个点的入度，如果一个点的入度为0，那么这个点依然存在于dict中，对应入度为0
    def get_indegree(self, graph):
        #初始化所有点的入度为0
        node_to_indegree = {x: 0 for x in graph}

        for node in graph:
            for neighbor in node.neighbors:
                node_to_indegree[neighbor] += 1
                
        return node_to_indegree
```
