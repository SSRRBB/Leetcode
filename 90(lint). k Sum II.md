## 题目：
Description
Given n unique postive integers, number k (1<=k<=n1<=k<=n) and target.

Find all possible k integers where their sum is target.

Example
```
Example 1:
Input:
array = [1,2,3,4]
k = 2
target = 5
Output:
[[1,4],[2,3]]
Explanation:
1+4=5,2+3=5
```
Example 2:
```
Input:
array = [1,3,4,6]
k = 3
target = 8
Output:
[[1,3,4]]
Explanation:
1+3+4=8
```
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/124.png)

## 思路：
DFS  组合

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/125.png)

## 答案：
```python
class Solution:
    """
    @param A: an integer array
    @param k: a postive integer <= length(A)
    @param target: an integer
    @return: A list of lists of integer
    """
    def kSumII(self, A, k, target):
        # write your code here
        #这里不需要sort,因为本题无需按照字母序，也无重复
        #需要sort的两种情况（意义）：
        # 1.可以按照字母序得到结果
        # 2.相同字母在一起，方便去重
        #A = sorted(A)
        subsets = []
        self.dfs(A, 0, k, target, [], subsets)
        return subsets
    # 递归的定义
    # 从A的index位置开始，选k个数放入subset，满足k个数之和为target    
    def dfs(self, A, index, k, target, subset, subsets):
        # 递归的出口
        # 找到k个数之和为target，记录答案，并立刻返回
        if k == 0 and target == 0:
            subsets.append(list(subset))
            return
        #同样是递归的出口（不可能找到结果）
        #1. 0个数字值和为非0target(如果已经完了数字，还没得到目标和)
        # 2.剩下数字之和为非负（规定的k个数字还没用完，但是和已经大于等于目标和）
        # 本题保证所有数字都是正整数。如果没有这个条件，#2不能return
        if k == 0 or target <= 0:
            return
        # 递归的拆解
        for i in range(index, len(A)):
            #把位置为i的数字加入subset
            subset.append(A[i])
            #从A 的i+1 位置开始，选k-1个数字放入subset
            self.dfs(A, i + 1, k - 1, target - A[i], subset, subsets)
            #回溯，把位置为i的数字移除
            subset.pop()

```
