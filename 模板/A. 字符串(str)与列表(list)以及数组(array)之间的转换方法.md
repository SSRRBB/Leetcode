## 前提：
```
list以及array是python中经常会用到的数据类型，当需要对list以及array进行文件的读写操作的时候，由于write函数参数需要的是一个str，所以这时就需要对list或者array进行str的转换了。

list和array的不同：
在进行转换之间先研究下python中list和array（np.array）的不同：

1、list是python中内置的数据类型，其中的数据的类型可以不相同，如java中List也可以不用相同的数据，但是为了格式的统一，就要用到泛型或者ArrayList。array中的数据类型必须是一样的。
2、list中保存的数据的存放地址，而不是数据，会增加内存的占用，所以存放数据还是尽量使用array。
3、list中有append的方法，可以进行追加，而array没有追加的方法，只能通过np.append来实现追加。
4、在print的时候，打印的结果不同。list元素之间有","分割，而array之间是空格。
```
```python
list = [1,2,3,4]
arr = np.array(list)
print(list) [1,2,3,4]
print(arr)  [1 2 3 3]

```
## 1.list转换为str  

**.join()**

1.1 当list中存放的数据是**字符串**时，一般是通过**str中的join函数**进行转换：

```python
list = ['a','b','c','d']
str1 = ''.join(list)
str2 = ' '.join(list)
str3 = '.'.join(list)
print(str1)  'abcd'
print(str2)  'a b'
print(str3)  'a.b.c.d'
```

1.2 但是当list中存放的**数据是整型数据或者数字**的话，需要先将**数据转换为字符串再进行转换**：

```python
list = [1, 2, 3, 4]
str1 = ''.join([str(x) for x in list])
str2 = ' '.join([str(x) for x in list])
str3 = '.'.join([str(x) for x in list])
print(str1)  '1234'
print(str2)  '1 2 3 4'
print(str3)  '1,2,3,4'
```

## 2. array转换为str

将array转换为str和list转换时是一样的，**join()函数中的参数是一个iterator**，所以array或者list都可以。

```python
list = ['a', 'b', 'c', 'd']
arr = np.array(list)
str = ''.join(arr)
print(str) 'abcd'
```

## 3. str转换为list 

**.split() // list()**

在将str转化为list时，主要就是通过**str的split()函数，split()参数为空时，默认以空格来做分割**。

直接通过**list转换时是以每一个字符为分割的。**

```python
str1 = 'abcde'
str4 = 'a,bcde'
str2 = 'a b c d e'
str3 = 'a, b, c, d, e'
result1 = list(str1)
result4 = list(str4)
result2 = str2.split()
result3 = str3.split(', ')
print(result1) ['a', 'b', 'c', 'd', 'e']
print(result4) ['a', ',', 'b', 'c', 'd', 'e']
print(result2) ['a', 'b', 'c', 'd', 'e']
print(result3) ['a', 'b', 'c', 'd', 'e']

```
