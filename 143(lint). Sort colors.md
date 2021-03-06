## 题目
Description
Given an array of n objects with k different colors (numbered from 1 to k), sort them so that objects of the same color are adjacent, with the colors in the order 1, 2, ... k.

You are not suppose to use the library's sort function for this problem.
k <= n

Example
```
Example1
Input: 
[3,2,2,1,4] 
4
Output: 
[1,2,2,3,4]
```
```
Example2
Input: 
[2,1,1,2,2] 
2
Output: 
[1,1,2,2,2]
```
Challenge
A rather straight forward solution is a two-pass algorithm using counting sort. That will cost O(k) extra memory. Can you do it O(logk) using extra memory?

## 思路
### **方法一 快速排序 彩虹排序（rainbow sort）**
使用分治法来解决。 传入两个区间，一个是颜色区间 color_from, color_to。另外一个是待排序的数组区间 index_from, index_to. 找到颜色区间的中点，将数组范围内进行 partition，<= color 的去左边，>color 的去右边。 然后继续递归。 时间复杂度 
O(nlogk) n是数的个数,k 是颜色数目。这是基于比较的算法的最优时间复杂度。
不基于比较的话，可以用计数排序（Counting Sort）
![p](https://github.com/SSRRBB/Leetcode/blob/main/Images/38.png)

![p](https://github.com/SSRRBB/Leetcode/blob/main/Images/40.png)

### **方法二  计数排序（counting sort）**
![p](https://github.com/SSRRBB/Leetcode/blob/main/Images/39.png)
## 答案
方法一
```python
class Solution:
    """
    @param colors: A list of integer
    @param k: An integer
    @return: nothing
    """
    def sortColors2(self, colors, k):
        # write your code here
        # 特殊情况处理
        if not colors or len(colors) < 2:
            return
        self.sort(colors, 1, k, 0, len(colors) - 1)

        # 递归三要素之一：递归的定义
    def sort(self, colors, color_from, color_to, index_from, index_to):
        #递归三要素之三：递归的出口
        #如果只有一个颜色，无需排序
        if color_from == color_to or index_from == index_to:
            return

        #递归三要素之二：递归的分解
        #寻找中间色，mid_color就是piviot
        mid_color = (color_from + color_to) // 2

        #分区partitionpatto,左边区域小于等于中间色，右边大约中间色
        left, right = index_from, index_to
        while left <= right:
            while left <= right and colors[left] <= mid_color:
                left += 1
            while left <= right and colors[right] > mid_color:
                right -= 1
            if left <= right:
                colors[left], colors[right] = colors[right], colors[left]
                left += 1
                right -= 1
        # 继续在子区域内按照颜色进行排序
        self.sort(colors, color_from, mid_color, index_from, right)
        self.sort(colors, mid_color + 1, color_to, left, index_to)

```


方法二
```python
class Solution:
    """
    @param colors: A list of integer
    @param k: An integer
    @return: nothing
    """
    def sortColors2(self, colors, k):
        size = len(colors)
        if (size <= 0):
            return

        index =  0
        while index < size:
            temp = colors[index] - 1
            #遇到计数位，跳过
            if colors[index] <= 0:
                index += 1
            else:
                #已经作为计数位
                if colors[temp] <= 0:
                    colors[temp] -= 1
                    colors[index] = 0
                    index += 1
                #还未被作为计数位使用
                else:
                    colors[index], colors[temp] = colors[temp], colors[index]
                    colors[temp] = -1       
        #倒着输出
        i = size - 1
        while k > 0:
            for j in range(-colors[k - 1]):
                colors[i] = k
                i -= 1
            k -= 1


```
