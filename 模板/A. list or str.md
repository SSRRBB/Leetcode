## tuple and string is immutable

## 1. slice: list 与 str通用 
**左闭右开**
```python
list = [0, 1, 2, 3, 4]

list[0:4] -> [0,1,2,3]
list[:4]  -> [0,1,2,3]
list[0:-1]-> [0,1,2,3]
list[:-1] -> [0,1,2,3]

list[:]   -> [0,1,2,3,4]

list[-1]  -> [4]

list[0:4:2] -> [0, 2]
```
**下面和3.联系起来了**
```
list[::1]  -> [0,1,2,3,4]
list[::-1] -> [4,3,2,1,0]
```

## 2. range: list 与 str通用 (类似slice)
**左闭右开**
```
range(n) #[0, 1, 2,……，n - 1] n个元素
range(m,n) #[m, 1, 2,……，n - 1]
range(m,n，k) #[m, m+k, m+2k,……，n - 1]
```
## 3. reverse() and sort()
**seq只能mutable的list**
```python
seq.reverse()  没有输出，但seq变了
seq.sort()     没有输出，但seq变了
```

**seq可以是 list， tuple和str**
```python
reversed(seq) 输出倒序seq,seq不变
sorted(seq)   输出排序seq,seq不变
```

## str的各种函数
**ASCII**
```
ord('a') 输入子树，输出数值
chr(asciinumber) 输入数值，输出字符]
```
**大小写变化**
```python
.lower()
.upper()

char = 'a'
char.upper() 输出A， char仍然是a  这一点和.sort()不一样
```
**输出bool value**
```python
.isdigit() 数字
.isalpha() 字母
.isalnum() 数字和字母
.islower() 小写
.isupper() 大写
.isspace() 空格
```

## shallow/deep copy
**python中的遍历储存的是地址而不是对象**


