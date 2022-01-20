## 题目：
You are given a string S of length  N containing only characters a and b. A substring (contiguous fragment) of 
S is called a semi-alternating substring if it does not contain three identical consecutive characters.
In other words, it does not contain either aaa or bbb substrings. Note that whole S is its own substring.

Write a function, which given a string S, returns the length of the longest semi-alternating substring of S.

Example 1
```
Input: "baaabbabbb"
Output: 7
Explanation: "aabbabb" is the longest semi-alternating substring.
```
Example 2
```
Input: "babba"
Output: 5
Explanation: Whole S is semi-alternating.
```
Example 3
```
Input: "abaaaa"
Output: 4
Explanation: "abaa" is the longest semi-alternating substring.
```

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/189.png)
## 思路：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/190.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/191.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/193.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/192.png)


## 答案：
```python
class Solution:
    """
    @param s: the string
    @return: length of longest semi alternating substring
    """
    def longestSemiAlternatingSubstring(self, s):
        # write your code here
        # 特殊情况
        if s is None or len(s) == 0:
            return 0
        # 特殊情况
        if len(s) < 3:  #k
            return len(s)

        # 符合条件的子串的的最大长度
        max_len = 0
        #末尾连续字母的cnt
        end_up_cnt = 1 # 因为我们的end从1开始
        #左指针,指向子串开始的位置
        start = 0
        #右指针，不断移动
        for end in range(1, len(s)):
            pre_char = s[end - 1]
            curr_char = s[end]

            if pre_char == curr_char:
                end_up_cnt += 1
                if end_up_cnt == 3: #k
                    #start指向重复出现三次的字母的第二个字母
                    start = end - 1 #end-(k-2)
                    #最后一个字母出现了3次
                    end_up_cnt = 2  # k-1
            else:
                #有一个新字母出现，出现次数更新为1
                end_up_cnt = 1

            max_len = max(max_len, end - start + 1)
        return max_len

```
