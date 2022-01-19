## 题目：
Description
Given a string which encode by ascii (For example, "ABC" can encode to "656667"),
You need to write a function that take an encoded string as input and returns reversed decoded string.

Example

Example1
```
Input: "7976766972"
Output: "HELLO"
```
Example2
```
Input: "656667"
Output: "CBA"
```

## 思路：
从后向前遍;并且把这对数字表示的字母加入字符串

ASCII: chr() int()



## 答案：
```python
class Solution:
    """
    @param encodeString: an encode string
    @return: a reversed decoded string
    """
    def reverseAsciiEncodedString(self, encodeString):
        # Write your code here
        ans = ''
        for i in range(len(encodeString) - 1, 0, -2):
            asciiNumber = int(encodeString[(i - 1): (i + 1)])
            ans += chr(asciiNumber)

        return ans

```
