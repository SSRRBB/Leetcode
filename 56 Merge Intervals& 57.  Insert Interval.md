## 题目：

https://leetcode.com/problems/merge-intervals/

## 思路：

时间复杂度： O(nlogn) 因为sort
空间复杂度：O(logn) 因为sort

```
1. 排序，这样pre的开始一定在cur的前面（6中情况变为三种）
2. 
  pre的结尾小于cur的开头，则将pre记录在res,并且开启新的pre;
  否则，合并
3.一定把最后一个pre append到res!!!!
```

## 答案：
```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals = sorted(intervals, key = lambda x : x[0])#按首位排序
        #intervals.sort()#默认也是按照首位排序。
        
        res = []
        pre = intervals[0]
        for cur in intervals[1:]:
            #如果不能合并(如果下一个开头在上一个结尾之后),则记录当前区间(加入到res)，并重新开辟区间
            if cur[0] > pre[1]:
                res.append(pre)
                pre = cur
            else:#否则，合并
                pre[1] = max(pre[1],cur[1])
        # 将最后一个区间加入
        res.append(pre)     
        return res
```
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/384.png)

## 题目：57. Insert Interval
https://leetcode.com/problems/insert-interval/

## 答案：
```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        if not intervals: 
            return [newInterval]
        n = len(intervals)
        res = []
        # 依次扫描区间数组，分三种情况
        i = 0
        # 不重叠，且区间在新区间的左边
        while i < n and  intervals[i][1] < newInterval[0]:
            res.append(intervals[i])
            i += 1

        # 重叠，进行合并
        while i < n and intervals[i][0] <= newInterval[1]:
            newInterval[0] = min(newInterval[0], intervals[i][0]) # 更新左边界
            newInterval[1] = max(newInterval[1], intervals[i][1]) # 更新右边界
            i += 1
        res.append(newInterval) # 更新完成后加入ans中

        # 不重叠，且区间在新区间的右边
        while i < n and  intervals[i][0] > newInterval[1]:
            res.append(intervals[i])
            i += 1
        return res
```
## 思路：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/386.png)