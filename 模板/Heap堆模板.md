## Heap 堆

- 底层的实现结构一般是**数组 list**
- **是一个完全二叉树，（从上到下，从左到右）**，但不是顺序的。
- **分为min heap 和max heap**
  - **只规定了上下大小，没有规定左右大小**

```
index从0开始
parent(i) = (i - 1) //2
leftchidl(i) = 2*i - 1
rightchidl(i) = 2*i + 1
```

## 不同语言对heap的实现
Python: heapq
Java: Priority Queue
C++: priority_queue

## code 常用
**构建堆O(N)**
```
import heapq
heapq.heapify(list)

# min heap
# index 从0开始
# 底层是list
```
**add O(N)；pop O(N);min/max O(1)**
```
heapq.heappush(heap, item)
heap.heappop(heap)
heap[0] # O(1)
```
**Romove any value:heapq支持O(N)**
**iterate heap:O(NlogN)**
