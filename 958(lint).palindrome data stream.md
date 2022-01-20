## 题目：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/187.png)


## 思路：
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/188.png)

## 答案：
```python

def getStream(self, s):
    if s is None or len(s) == 0:
        return None
    #存放在任意index,是否可以组成回文串
    res = [0 for _ in range(len(s))]
    #记录出现奇数次的字母的个数
    odd_letter_count = 0
    #记录每个字母出现的次数
    letters = [0 for _ in range(26)]
      
    for i in range(len(s)):
        #拿到一个新字母更新出现的次数
        letters[ord(s[i]) - ord('a')] += 1
        #如果此字母出现基数词，odd_letter_count 加一
        if letters[ord(s[i]) - ord('a')] % 2 == 1：
            odd_letter_cnt += 1
        else:
           odd_letter_cnt -= 1
      
         #如果只有一个字母或者0个字母出现了奇数词，那么可以组成回文串
        res[i] = 0 if odd_letter_cnt > 1 else 1
    
    return res
     
    


```
