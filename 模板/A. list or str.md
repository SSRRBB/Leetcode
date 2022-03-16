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

## python 变量：address vs object
**python的变量variable储存的是对象object的地址address而不是对象object本身**
**或者说python中所有的变量都是引用/address**

**赋值操作assign和函数传参都是复制地址copy address

**修改引用adress vs 修改对象object**
```python
# 修改引用adress
# l1和l2都为对象，但是都指向相同地址
l1 = [1, 2, 3, 4]
l2 = l1
l2[0] = 100
print(l1) [100, 2, 3, 4]
print(l2) [100, 2, 3, 4]
```

```python
# num1 地址指向对象10;开始num2地址指向对象10，后来num2地址指向对象20
num1 = 10
num2 = num1
num2 = 20
print(num1)  10
print(num2)  20
```
## shallow copy:直接赋值assign = 和list.append()
**只copy了对象的引用address，并没有copy对象oject**
```python
l1 = [1, 2, 3, 4]
l2 = l1
l1[0] = 100
print(l1) [100, 2, 3, 4]
print(l2) [100, 2, 3, 4]
```
```python
list = [2]
x = [1, 2, 3]
list.append(x)
print(list)  [2, [1, 2, 3]]

x[1] = 0
print(list)  [2, [1,0, 3]]

id(x) == id(list[1]) True

```

