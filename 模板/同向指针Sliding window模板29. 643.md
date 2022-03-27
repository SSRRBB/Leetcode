## 题目：209. Minimum Size Subarray Sum
Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.


Example 1:
```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```
Example 2:
```
Input: target = 4, nums = [1,4,4]
Output: 1
```
Example 3:
```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```
 

Constraints:
```
1 <= target <= 109
1 <= nums.length <= 105
1 <= nums[i] <= 105
```

## 思路：

### 同向指针Sliding window模板 (12道题目)
```python
class Solution:
    def problemName(self, s: str) -> int:
        # Step 1: 定义需要维护的变量们 (对于滑动窗口类题目，这些变量通常是最小长度，最大长度，或者哈希表)
        x, y = ..., ...

        # Step 2: 定义窗口的首尾端 (start, end)， 然后滑动窗口
        start = 0
        for end in range(len(s)):
            # Step 3: 更新需要维护的变量, 有的变量需要一个if语句来维护 (比如最大最小长度)
            x = new_x
            if condition:
                y = new_y

            '''
            ------------- 下面是两种情况，读者请根据题意二选1 -------------
            '''
            # Step 4 - 情况1
            # 如果题目的窗口长度固定：用一个if语句判断一下当前窗口长度是否达到了限定长度 
            # 如果达到了，窗口左指针前移一个单位，从而保证下一次右指针右移时，窗口长度保持不变, 
            # 左指针移动之前, 先更新Step 1定义的(部分或所有)维护变量 
            if 窗口长度达到了限定长度:
                # 更新 (部分或所有) 维护变量 
                # 窗口左指针前移一个单位保证下一次右指针右移时窗口长度保持不变

            # Step 4 - 情况2
            # 如果题目的窗口长度可变: 这个时候一般涉及到窗口是否合法的问题
            # 如果当前窗口不合法时, 用一个while去不断移动窗口左指针, 从而剔除非法元素直到窗口再次合法
            # 在左指针移动之前更新Step 1定义的(部分或所有)维护变量 
            while 不合法:
                # 更新 (部分或所有) 维护变量 
                # 不断移动窗口左指针直到窗口再次合法

        # Step 5: 返回答案
        return ...

```
## 题目：643. Maximum Average Subarray I(窗口长度固定, easy)
https://leetcode.com/problems/maximum-average-subarray-i/

## 答案 643
```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        # Step 1:定义需要维护的变量
        # 本题求最大平均值 (其实就是求最大和)，所以需要定义curr_sum, 同时定义一个max_avg (初始值为负无穷)
        max_avg = float('-inf')
        curr_sum = 0
        # Step 2: 定义窗口的首尾端 (start, end)， 然后滑动窗口
        start = 0
        for end in range(len(nums)):
            # Step 3: 更新需要维护的变量 (curr_sum, max_avg), 不断把当前值积累到curr_sum上
            curr_sum += nums[end]
            # if end - start + 1 == k:
            #     max_avg = max(max_avg, curr_sum / k)
            # # Step 4 根据题意可知窗口长度固定，所以用if
            # # 窗口首指针前移一个单位保证窗口长度固定, 同时提前更新需要维护的变量 (curr_num)
            # if end - start + 1 >= k:
            #     curr_sum -= nums[start]
            #     start += 1
            
            ## 个人认为此题把 step 3和 4合并更好。step 4 if 其实还是  end - start + 1 == k
            if end - start + 1 == k:
                max_avg = max(max_avg, curr_sum / k)
                curr_sum -= nums[start]
                start += 1
        return max_avg
            
```
### 代码回想录
**滑动窗口的精髓就是动态调节滑动窗口的起始位置：根据子序列之和**
**滑动窗口三要素**
```
## 窗口内是什么?curr_sum
## 如何移动窗口的起始位置start？start = 0:根据子序列之和动态调节start位置
## 如何移动窗口的终止位置end？ for end in range(len(nums))
```
时间复杂度：O(n)，其中 n 是数组的长度。指针 start 和 end 最多各移动 n 次。
空间复杂度：O(1)。

## 答案 209：
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        ##同向双指针sliding window
        min_len = float('inf')
        curr_sum = 0
        
        start = 0 
        for end in range(len(nums)):
            curr_sum += nums[end]
            # 这一段可以删除，因为下面的while已经handle了这一块儿逻辑，不过写在这也没影响
            # if curr_sum >= target:
            #     min_len = min(min_len, end - start + 1)
            while curr_sum >= target:
                min_len = min(min_len, end - start + 1 )
                curr_sum -= nums[start]
                start += 1
                
        return 0 if min_len == float('inf') else min_len



```

# 滑动窗口（Sliding Window）
Github azl397985856; 力扣：力扣加加

笔者最早接触滑动窗口是`滑动窗口协议`，滑动窗口协议（Sliding Window Protocol），属于 TCP 协议的一种应用，用于网络数据传输时的流量控制，以避免拥塞的发生。 发送方和接收方分别有一个窗口大小 w1 和 w2。窗口大小可能会根据网络流量的变化而有所不同，但是在更简单的实现中它们是固定的。窗口大小必须大于零才能进行任何操作。

我们算法中的滑动窗口也是类似，只不过包括的情况更加广泛。实际上上面的滑动窗口在某一个时刻就是固定窗口大小的滑动窗口，随着网络流量等因素改变窗口大小也会随着改变。接下来我们讲下算法中的滑动窗口。

## 介绍

滑动窗口是一种解决问题的思路和方法，通常用来解决一些连续问题。 比如 LeetCode 的 [209. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/solution/209-chang-du-zui-xiao-de-zi-shu-zu-hua-dong-chua-2/)。更多滑动窗口题目见下方`题目列表`。

## 常见套路

滑动窗口主要用来处理连续问题。比如题目求解“连续子串 xxxx”，“连续子数组 xxxx”，就应该可以想到滑动窗口。能不能解决另说，但是这种敏感性还是要有的。

从类型上说主要有：

- 固定窗口大小
- 窗口大小不固定，求解最大的满足条件的窗口
- 窗口大小不固定，求解最小的满足条件的窗口（上面的 209 题就属于这种）

后面两种我们统称为`可变窗口`。当然不管是哪种类型基本的思路都是一样的，不一样的仅仅是代码细节。

### 固定窗口大小

对于固定窗口，我们只需要固定初始化左右指针 l 和 r，分别表示的窗口的左右顶点，并且保证：

1. l 初始化为 0
2. 初始化 r，使得 r - l + 1 等于窗口大小
3. 同时移动 l 和 r
4. 判断窗口内的连续元素是否满足题目限定的条件
   - 4.1 如果满足，再判断是否需要更新最优解，如果需要则更新最优解
   - 4.2 如果不满足，则继续。

![](https://tva1.sinaimg.cn/large/007S8ZIlly1ghlugkc80jj308z0d5aaa.jpg)

### 可变窗口大小

对于可变窗口，我们同样固定初始化左右指针 l 和 r，分别表示的窗口的左右顶点。后面有所不同，我们需要保证：

1. l 和 r 都初始化为 0
2. r 指针移动一步
3. 判断窗口内的连续元素是否满足题目限定的条件
   - 3.1 如果满足，再判断是否需要更新最优解，如果需要则更新最优解。并尝试通过移动 l 指针缩小窗口大小。循环执行 3.1
   - 3.2 如果不满足，则继续。

形象地来看的话，就是 r 指针不停向右移动，l 指针仅仅在窗口满足条件之后才会移动，起到窗口收缩的效果。

![](https://tva1.sinaimg.cn/large/007S8ZIlly1ghlugl94y8j30d90d50t5.jpg)

## 模板代码

### 伪代码

```
初始化慢指针 = 0
初始化 ans

for 快指针 in 可迭代集合
   更新窗口内信息
   while 窗口内不符合题意
      扩展或者收缩窗口
      慢指针移动
   更新答案
返回 ans
```

### 代码

以下是 209 题目的代码，使用 Python 编写，大家意会即可。

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        l = total = 0
        ans = len(nums) + 1
        for r in range(len(nums)):
            total += nums[r]
            while total >= s:
                ans = min(ans, r - l + 1)
                total -= nums[l]
                l += 1
        return  0 if ans == len(nums) + 1 else ans
```

## 题目列表（有题解）

以下题目有的信息比较直接，有的题目信息比较隐蔽，需要自己发掘

- [【Python，JavaScript】滑动窗口（3. 无重复字符的最长子串）](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/solution/pythonjavascript-hua-dong-chuang-kou-3-wu-zhong-fu/)
- [76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/solution/python-hua-dong-chuang-kou-76-zui-xiao-fu-gai-zi-c/)
- [209. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/solution/209-chang-du-zui-xiao-de-zi-shu-zu-hua-dong-chua-2/)
- [【Python】滑动窗口（438. 找到字符串中所有字母异位词）](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/solution/python-hua-dong-chuang-kou-438-zhao-dao-zi-fu-chua/)
- [【904. 水果成篮】（Python3）](https://leetcode-cn.com/problems/fruit-into-baskets/solution/904-shui-guo-cheng-lan-python3-by-fe-lucifer/)
- [【930. 和相同的二元子数组】（Java，Python）](https://leetcode-cn.com/problems/binary-subarrays-with-sum/solution/930-he-xiang-tong-de-er-yuan-zi-shu-zu-javapython-/)
- [【992. K 个不同整数的子数组】滑动窗口（Python）](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/solution/992-k-ge-bu-tong-zheng-shu-de-zi-shu-zu-hua-dong-c/)
- [978. 最长湍流子数组](../problems/978.longest-turbulent-subarray.md)
- [【1004. 最大连续 1 的个数 III】滑动窗口（Python3）](https://leetcode-cn.com/problems/max-consecutive-ones-iii/solution/1004-zui-da-lian-xu-1de-ge-shu-iii-hua-dong-chuang/)
- [【1234. 替换子串得到平衡字符串】[Java/C++/Python] Sliding Window](https://leetcode.com/problems/replace-the-substring-for-balanced-string/discuss/408978/javacpython-sliding-window/367697)
- [【1248. 统计「优美子数组」】滑动窗口（Python）](https://leetcode-cn.com/problems/count-number-of-nice-subarrays/solution/1248-tong-ji-you-mei-zi-shu-zu-hua-dong-chuang-kou/)
- [1658. 将 x 减到 0 的最小操作数](../problems/1658.minimum-operations-to-reduce-x-to-zero.md)

## 扩展阅读

- [LeetCode Sliding Window Series Discussion](https://leetcode.com/problems/binary-subarrays-with-sum/discuss/186683/)
