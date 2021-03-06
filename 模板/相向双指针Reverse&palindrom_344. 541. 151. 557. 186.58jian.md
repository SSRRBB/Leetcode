# String
## 题目：344.Reverse String
Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

Example 1:
```
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```
Example 2:
```
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

**lintcode**
Description
Write a function that takes a string as input and returns the string reversed.

Example 1：
```
Input："hello"
Output："olleh"
```
Example 2：
```
Input："hello world"
Output："dlrow olleh"
```

## 思路：
**相向向双指针：reverse**

**把string转成list(因为string是immutable的)**

**str to list/list to str(详细看字符串(str)与列表(list)以及数组(array)之间的转换方法详细整)**
```
时间复杂度：O(N),其中 N 为字符数组的长度。一共执行了 N/2 次的交换。
空间复杂度：O(1)。只使用了常数空间来存放若干变量。 双指针
```

## 答案：
**leetcode**
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
        
        #return s.reverse() # 一行程序
```
**lintcode**
```python
class Solution:
    """
    @param s: a string
    @return: return a string
    """
    def reverseString(self, s):
        # write your code here
        aList = list(s)
        print(aList)
        left, right = 0, len(aList) - 1
        while left < right:
            aList[left], aList[right] = aList[right], aList[left]
            left += 1
            right -= 1
        
        return ''.join(aList)      
```
## 题目 541. Reverse String II
Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

Example 1:
```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```
Example 2:
```
Input: s = "abcd", k = 2
Output: "bacd"
```
Constraints:
```
1 <= s.length <= 104
s consists of only lowercase English letters.
1 <= k <= 104
```
```
题目描述：给定一个字符串 s 和一个整数 k，你需要对从字符串开头算起的每隔 2k 个字符的前 k 个字符进行反转。

如果剩余字符少于 k 个，则将剩余字符全部反转。
如果剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符，其余字符保持原样。
```

## 思路：
**1. 字符块为2k（遍历步长为2k**

**2. 反转要求：我们要反转前k个，不足k全部反转，即我们需要确定反转区域的左右索引。
所以：左边界为i，右边界为i + k - 1和length - 1的最小值（满足前k个反转前k个，否则反转剩余的字符）**

**#ls[i:i+k] = reversed(ls[i:i+k])   # 用库的话这一步就解决了**
## 答案：
```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        ls = list(s) # 变成list
        
        for i in range(0, len(ls), 2 * k):
        #ls[i:i+k] = reversed(ls[i:i+k])   # 用库的话这一步就解决了
            left = i
            right = min(i + k - 1, len(ls) - 1)
            
            while left < right:
                ls[left], ls[right] = ls[right], ls[left]
                left += 1
                right -= 1
        
        return ''.join(ls) # 变回str
```
## 题目：151. Reverse Words in a String
Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.


Example 1:
```
Input: s = "the sky is blue"
Output: "blue is sky the"
```
Example 2:
```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```
Example 3:
```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

Constraints:

1 <= s.length <= 104
s contains English letters (upper-case and lower-case), digits, and spaces ' '.
There is at least one word in s.
## 思路：
**方法三记一下，因为后面题目要用**
## 答案：
# 方法一和二：

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/176.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/177.png)

# 方法三：

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/178.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/179.png)


## 答案：
**方法一&二**
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        #"Hello World"
        # s.split() 将字符串分割成单词列表 ["Hello" ,"World"] **并且可以去掉中间和多余空格**
        # reversed 或者[::-1]  然后整个单词列表反转["World","Hello"]
        # " ".join 单词列表 变为字符串
         return ' '.join(reversed(s.split()))
         #return ' '.join(s.split()[::-1])
```
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        #"Hello World"
        # s.split() 将字符串分割成单词列表 ["Hello" ,"World"] **并且可以去掉中间和多余空格**
        # 用双指针代替 reversed 或者[::-1]  然后整个单词列表反转["World","Hello"]
        # " ".join 单词列表 变为字符串
        
        ls = s.split()

        left, right = 0, len(ls) - 1
        while left < right:
            ls[left], ls[right] = ls[right], ls[left]
            left += 1
            right -= 1
        
        return ' '.join(ls)
```
**方法三**
```python
class Solution:
    def reverseWords(self, s: str) -> str:
     # 去掉头尾空格和中间多余空格
        l = self.trim_spaces(s)
        # 翻转字符串
        self.reverse(l, 0, len(l) - 1)
        # 翻转每个单词
        self.reverse_each_word(l)
        
        return ''.join(l)

    def trim_spaces(self, s: str) -> list:
        left, right = 0, len(s) - 1
        # 去掉字符串开头的空白字符
        while left <= right and s[left] == ' ':
            left += 1
        
        # 去掉字符串末尾的空白字符
        while left <= right and s[right] == ' ':
            right -= 1
        
        # 将字符串间多余的空白字符去除
        output = []
        while left <= right:
            if s[left] != ' ':
                output.append(s[left])
            elif output[-1] != ' ':
                output.append(s[left])
            left += 1
            
        return output
            
    def reverse(self, l: list, left: int, right: int) -> None:
        while left < right:
            l[left], l[right] = l[right], l[left]
            left, right = left + 1, right - 1
            
    def reverse_each_word(self, l: list) -> None:
        n = len(l)
        start = end = 0
        
        while start < n:
            # 循环至单词的末尾
            while end < n and l[end] != ' ':
                end += 1
            # 翻转单词
            self.reverse(l, start, end - 1)
            # 更新start，去找下一个单词
            start = end + 1
            end += 1
```

## 题目：557. Reverse Words in a String III

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example 1:
```
Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```
Example 2:
```
Input: s = "God Ding"
Output: "doG gniD"
```

Constraints:
```
1 <= s.length <= 5 * 104
s contains printable ASCII characters.
s does not contain any leading or trailing spaces.
There is at least one word in s.
All the words in s are separated by a single space.
```
## 思路：

**方法一（类似151方法一）：**
```
s.split()   word[::-1]  " ".join 
        # "God Ding"  
        # s.split() 将字符串分割成单词列表 ["God" ,"Ding" ]
        # word[::-1] 然后把每个单词反转切片 ["doG","ginD"]
        # " ".join 单词列表 变为字符串
```
**方法二类似方法一（类似151方法二）：**
```
# "God Ding"  
# .split() 将字符串分割成单词列表 ["God" ,"Ding" ]
# 用双指针代替word[::-1]方法: 把每个单词反转切片 ["doG","ginD"]
# " ".join 单词列表 变为字符串
```
**方法三（类似151方法三）： **
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/181.png)

## 答案：
**方法一**
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        
        # "God Ding"  
        # s.split() 将字符串分割成单词列表 ["God" ,"Ding" ]
        # word[::-1] 然后把每个单词反转切片 [["doG","ginD" ]]
        # " ".join 单词列表 变为字符串
        
        return " ".join([word[::-1] for word in s.split()])
        
        #一行拆解：
        ans = []
        for word in s.split():
            ans.append(word[::-1])
            
        return ' '.join(ans)

```
**方法二**
```python
        ls = s.split()
        
        ans = []
        for word in ls:
            ans.append(self.reverseString(word))
        
        return ' '.join(ans)
  
    def reverseString(self, word):
        lsword = list(word) # 变成list
        left, right = 0, len(lsword) - 1
        while left < right:
            lsword[left], lsword[right] = lsword[right], lsword[left]
            left += 1
            right -= 1
        return ''.join(lsword)

```
**方法三**
```python

        l = list(s)

        # 翻转每个单词
        self.reverse_each_word(l)
        
        return ''.join(l)

    def reverse(self, l: list, left: int, right: int) -> None:
        while left < right:
            l[left], l[right] = l[right], l[left]
            left, right = left + 1, right - 1
            
    def reverse_each_word(self, l: list) -> None:
        n = len(l)
        start = end = 0
        
        while start < n:
            # 循环至单词的末尾
            while end < n and l[end] != ' ':
                end += 1
            # 翻转单词
            self.reverse(l, start, end - 1)
            # 更新start，去找下一个单词
            start = end + 1
            end += 1

```

## 题目：186. Reverse Words in a String II
Given a character array s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by a single space.

Your code must solve the problem in-place, i.e. without allocating extra space.

 
Example 1:
```
Input: s = ["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"]
Output: ["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
```
Example 2:
```
Input: s = ["a"]
Output: ["a"]
```

Constraints:
```
1 <= s.length <= 105
s[i] is an English letter (uppercase or lowercase), digit, or space ' '.
There is at least one word in s.
s does not contain leading or trailing spaces.
All the words in s are guaranteed to be separated by a single space.
```
## 思路：
**（类似151方法三: **
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/180.png)
## 答案：
```python
class Solution:
    def reverseWords(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
    
        # 翻转字符串
        self.reverse(s, 0, len(s) - 1)
        # 翻转每个单词
        self.reverse_each_word(s)
        
            
    def reverse(self, s: list, left: int, right: int) -> None:
        while left < right:
            s[left], s[right] = s[right], s[left]
            left, right = left + 1, right - 1
            
    def reverse_each_word(self, s: list) -> None:
        n = len(s)
        start = end = 0
        
        while start < n:
            # 循环至单词的末尾
            while end < n and s[end] != ' ':
                end += 1
            # 翻转单词
            self.reverse(s, start, end - 1)
            # 更新start，去找下一个单词
            start = end + 1
            end += 1
```
## 题目：剑指 Offer 58 - II. 左旋转字符串
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

```
示例 1：

输入: s = "abcdefg", k = 2
输出: "cdefgab"
示例 2：

输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"。
```
## 思路:
```
反转区间为前n的子串
反转区间为n到末尾的子串
反转整个字符串
```
**时间复杂度：O(n)**

**空间复杂度：O(n)，python的string为不可变，需要开辟同样大小的list空间来修改**

## 答案：
```python
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        ## return s[n:len(s)] + s[0: n]
```
```python
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        ## return s[n:len(s)] + s[0: n]
        ls = list(s)
        self.reverseSub(ls, 0, n-1)
        self.reverseSub(ls, n, len(ls) - 1)
        self.reverseSub(ls, 0, len(ls) - 1)
        return ''.join(ls)

    def reverseSub(self, ls, left, right):
        while left < right:
            ls[left], ls[right] = ls[right], ls[left]
            left += 1
            right -= 1
```
# Palindrome
## 题目 125 Valid Palindrome
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

 
Example 1:
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```
Example 2:
```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```
Example 3:
```
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```
## 思路
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/184.png)
**判断一个字符串，忽略大小写和非法字符之后是否是一个回文串**
**.lower() .upper() .isdigit() .isalpha() is.alnum()**

时间o(n)
空间o(1）
## 答案
**更简单的方法 .isalnum()**
```python
class Solution:
    
    def isPalindrome(self, s: str) -> bool:
        left, right = 0, len(s) - 1
        while left < right:
            while left < right and not s[left].isalnum():
                left += 1
            while left < right and not s[right].isalnum():
                right -= 1
            if left < right and s[left].lower() !=  s[right].lower():
                return False
            left += 1
            right -= 1
        return True
```
```python
class Solution:
    
    def isPalindrome(self, s: str) -> bool:
        left , right = 0, len(s) - 1
        while left < right:
            while left < right and not self.is_valid(s[left]):
                left += 1
            while left < right and not self.is_valid(s[right]):
                right -= 1
            if left < right and s[left].lower() != s[right].lower():
                return False
            left += 1
            right -=1
            
        return True
                 
            
    def is_valid(self, char):
        return char.isdigit() or char.isalpha()
    
    #不可以创建新字符串（空间复杂度）
    #时间复杂度（o(n)）

```

## 题目 680 Valid Palindrome II
Given a string s, return true if the s can be palindrome after deleting at most one character from it.

Example 1:
```
Input: s = "aba"
Output: true
```
Example 2:
```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```
Example 3:
```
Input: s = "abc"
Output: false
```
## 思路
是否可以在去掉一个字符的情况下是一个回文串，abca可以，abc不可以

基本思想是沿袭令狐老师的solution.在具体做法上，一旦遇到不想等的字符，就直接越过一个字符进行判断。 理解起来更直观一点儿。

## 答案
```python
class Solution:
    def validPalindrome(self, s: str) -> bool:

        left, right =0,  len(s) - 1 
        while left < right:#<=也可以
            if s[left] == s[right]:
                left += 1 
                right -= 1 
            else:
                return self.helper(s, left, right - 1) or self.helper(s, left + 1, right)
        
        return True
                
                
    def helper(self, s, left, right):
        while left < right:#<=也可以
            if s[left] != s[right]:
                return False 
        
            left += 1 
            right -= 1 
        
        return True
```
#令狐冲
```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        if not s:
            return False
        
        left, right = self.findDifference(s, 0 , len(s) - 1)
        if left >= right: #这是个重要判断条件
            return True

        return self.isPalindrome(s, left + 1, right) or self.isPalindrome(s, left, right - 1)

    def isPalindrome(self, s, left, right):
        left, right  = self.findDifference(s, left, right)
        return left >= right

    def findDifference(self, s, left, right):
        while left < right:
            if s[left] != s[right]:
                return left, right
            left += 1
            right -= 1

        return left, right

```
