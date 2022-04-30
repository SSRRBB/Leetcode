## Hea 堆常用来求top K 问题
```
heapq.heapify(list) 堆化 O(N)

heapq.heappop(heap) 弹出并返回栈顶最小值 O(N),注意indexerror

heapq.heappush(heap, item) heap定义堆、item增加的元素 O(n)

heap[0] 值访问栈顶，但不弹出min/max O(1)

Romove any value:heapq支持O(N)

iterate heap:O(NlogN)
```
**构建堆O(N)**
```
import heapq
heapq.heapify(list)

# min heap
# index 从0开始
# 底层是list
```

## key = lambda x:x[i]
```
## tuple
a = [(2, 29), (5, 58), (1, 70)]
a.sort(key = lambda x:x[0])
print(a) [(1, 70), (2, 29), (5, 58)]
a.sort(key = lambda x:x[1])
print(a) [(2, 29), (5, 58), (1, 70)]
```
```hashmap= {2:29 , 5:58, 1: 70}
print(sorted(hashmap.items(), key = lambda x:(x[1], x[0])))
[(2, 29), (5, 58), (1, 70)]    hashmap value 

hashmap= {2:29 , 5:58, 1: 70}
print(sorted(hashmap.items(), key = lambda x:(x[0], x[1])))
[(1, 70), (2, 29), (5, 58)]  hashmap key

#细节
## hashmap key
hashmap= {2:29 , 5:58, 1: 70}
print(sorted(hashmap)) [1, 2, 5]
print(sorted(hashmap.keys())) [1, 2, 5]

hashmap= {2:29 , 5:58, 1: 70}
for i in sorted(hashmap): 
    print((i, hashmap[i])) 
(1, 70)
(2, 29)
(5, 58)

## hashmap value:
hashmap= {2:29 , 5:58, 1: 70}
print(sorted(hashmap.values())) [29, 58, 70]

```
## 题目 347. Top K Frequent Elements
https://leetcode.com/problems/top-k-frequent-elements/
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```
Example 2:
```
Input: nums = [1], k = 1
Output: [1]
```
Constraints:
```
1 <= nums.length <= 105
k is in the range [1, the number of unique elements in the array].
It is guaranteed that the answer is unique.
```

Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
## 思路：
方法一 hashmap key = lambda x:(x[0], x[1])
## 答案：
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        #哈希表排序nlogn
        hashmap = collections.Counter(nums)
        hashmap_sort = sorted(hashmap.items(), key = lambda x:(x[1], x[0]))
        hashmap_sort.reverse()
        res = []
        for i in range(k):
            res.append(hashmap_sort[i][0])
        return res
```
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        #堆nlogk,创建heap时候，维持了heap是k
        heap = []
        hashmap = collections.Counter(nums)
        for key, value in hashmap.items():
            heapq.heappush(heap, (value, key))
            if len(heap) > k: #默认是最小堆，这里维持了heap大小为k,把小的输出
                heapq.heappop(heap)
        #因为说顺序没有关系
        return [items[1] for items in heap]
```


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


**heapq.heapify(list) 堆化 O(N)**

**heapq.heappop(heap) 弹出并返回栈顶最小值 O(N),注意indexerror**

**heapq.heappush(heap, item) heap定义堆、item增加的元素 O(n)**

**heap[0] 值访问栈顶，但不弹出min/max O(1)**

**Romove any value:heapq支持O(N)**

**iterate heap:O(NlogN)**

**构建堆O(N)**
```
import heapq
heapq.heapify(list)

# min heap
# index 从0开始
# 底层是list
```

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/214.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/376.jpeg)
