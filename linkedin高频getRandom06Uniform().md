## 题目：linkedin高频:
Input:
A method getRandom01Biased() that generates a random integer in [0, 1], 
where 0 is generated with probability p and 1 is generated with probability (1-p)
Output:
A method getRandom06Uniform() that generates a random integer in [0, 6] with uniform probability
follow up: a method getRandomUniform(int a, int b) that generates a random integer in [a, b) with uniform probability

# 类似 470
## 答案：
**答案**
```python
#A method getRandom01Biased() that generates a random integer in [0, 1], where 0 is generated with probability p and 1 is generated with probability (1-p).
#A method getRandom06Uniform() that generates a random integer in [0, 6] with uniform probability.
#A method getRandomUniform(int a, int b) that generates a random integer in [a, b] with uniform probability.

###这个functon解释同上面(#从有偏见的硬币产生公平的结果)
def getUniform():
    while True:
        randNum1 = getRandom01Biased()
        randNum2 = getRandom01Biased()
            if randNum1 != randNum2:
                return randNum1

##这个function a random integer in [0, 6] with uniform probability
def getRandom06Uniform():
    while True:
        randNum1 = getUniform()
        randNum2 = getUniform()
        randNum3 = getUniform()
        result = (randNum1 << 2) + (randNum2 << 1) + randNum3
        if result != 7:
            return result
#print(0 << 1)#0
#print(1 << 1) #2
#print(0 << 2)# 0
#print(1 << 2)#4
## 这个方程生成【a,b】
def getRandomUniform(a, b):
    numDigit = 0
    while (1 << numDigit) <= b-a:
        numDigit += 1
    while True:
        result = 0
        for i in range(numDigit):
            result += (getUniform() << i)
        if result <= b - a:
            return result + a
```
## 题目：
Question: Write a function that simulates an M sided dice given the probability of each side showing up
Input:
List of p_i, where p_i indicates probability of face i showing up. i={1, 2, ..., M} (M >= 1)
Output:
1 sample from this dice: index of the face that shows up

Example
input: [0.1, 0.5, 0.3, 0.1]
Run the function 5 times,
output: 2, 1, 2, 2, 3

**生成有偏见的dice,2 面， M 面**
https://360ai.org/question/479236.html
如何在 python 中模拟偏向模具
## 答案：
```python
import random
def get2biasDice(a): ## [0.1, 0.9] #[p, 1 - p]
    #input = a = [0.1, 0.9] or [p, 1 - p]
    m = len(a)
    p = a[0]
    tail = 0
    head = 1
    r = random.random() #[0, 1)
    # r = 0. 7
    if r < p: 
        return tail
    else: #0.7 > 0.1
        return head 
a = [0.5, 0.5] 
print(get2biasDice(a))


import random   
def gemMbiasDice(a): 
    # input: [0.1, 0.5, 0.3, 0.1]
    m = len(a)   
    randRoll = random.random() # in [0,1]
    cur_sum = 0
    res = 1
    for p in a:
        cur_sum += p
        if randRoll < cur_sum:
            return res
        res +=1
        
a = [0.1, 0.5, 0.3, 0.1]   
print(gemMbiasDice(a))

```
## 题目1 and 2 结合：
**从有偏见的硬币产生公平的结果**
```
#https://www.techiedelight.com/zh/generate-fair-results-biased-coin/
from random import randint
 

 
# 一个有偏函数，它以 80% 概率返回 TAILS，并且
# HEADS 概率为 20%
def biased():
    HEADS, TAILS = 1, 0
    # 生成一个介于 0-99 之间的随机数，包括两者
    r = randint(0, 99)
 
    # 如果我们得到 [0-79] 之间的数字，# 返回 TAILS；否则，返回 HEADS
    return TAILS if (r <= 79) else HEADS
 
 
# 使用指定函数以相等的概率返回 HEADS 和 TAILS
def generate():
    while True:
        first = biased()
        second = biased()
        if first != second:
            return first    #或返回second
 
 
if __name__ == '__main__':
 
    x = y = 0
    for i in range(100000):
        val = generate()
        if val > 0:
            x += 1
        else:
            y += 1
 
    print('HEADS ~', x / 1000, '%')        # ~50%
    print('TAILS ~', y / 1000, '%')        # ~50%
```
**测一测**
```python
import random import randint

def rand2(): #[0, 1]
    r = randint(0, 1)
    return r

    
def getRandom06Uniform():
    while True:
#         res = 2 *(2 * rand2() + rand2()) + rand2() #[0,1,2,3,4,5,6,7]#因为2 * rand2() + rand2()生成等概率【0，1，2，3】#
#         if res < 7:
#             return res
# #         return getRandom06Uniform()
        res = (rand2() << 2) + (rand2() << 1) + rand2() #[0,1,2,3,4,5,6,7]
        if res < 7:
            return res
        
if __name__ == '__main__':
 
    x = y = z = a = b = c = d = 0
    for i in range(100000):
        val = getRandom06Uniform()
        if val == 0:
            x += 1
        if val == 1:
            y += 1
        if val == 2:
            z += 1
        if val == 3:
            a += 1
        if val == 4:
            b += 1
        if val == 5:
            c += 1 
        if val == 6:
            d += 1
    print('0 ~', x / 100000, '%')        # ~14%
    print('1 ~', y / 100000, '%')        # ~14%
    print('2 ~', z / 100000, '%')        # ~14%     
    print('3 ~', a / 100000, '%')        # ~14% 
    print('4 ~', b / 100000, '%')        # ~14%
    print('5 ~', c / 100000, '%')        # ~14%
    print('6 ~', d / 100000, '%')        # ~14%

```
**#Implement rand3() using rand2()[0,1]生成[0,1,2]**
```python
#Implement rand3() using rand2()
#Given a function rand2() that returns 0 or 1 with equal probability, 
#implement rand3() using rand2() that returns 0, 1 or 2 with equal probability.

# Python3 Program to print 0, 1 or 2 with equal
# Probability
 
from random import randint
# Random Function to that returns 0 or 1 with
# equal probability
 
def rand2(): #[0, 1]
    r = randint(0, 1)
    return r

def rand3(): #[0, 1, 2]
    while True:
        res = 2 * rand2() + rand2() #[0, 1, 2 ,3]
        if res < 3:
            return res
        return rand3()
 
if __name__ == '__main__':
 
    x = y = z = 0
    for i in range(100000):
        val = rand3()
        if val == 0:
            x += 1
        if val == 1:
            y += 1
        if val == 2:
            z += 1
       
 
    print('0 ~', x / 100000, '%')        # ~33%
    print('1 ~', x / 100000, '%')        # ~33%
    print('2 ~', x / 100000, '%')        # ~33%
```

## sampling with givin PMF
idea is to translate pmf to cdf and then use inverse to draw samples 

PMF https://www.probabilitycourse.com/chapter3/3_1_3_pmf.php 
CDF https://www.probabilitycourse.com/chapter3/3_2_1_cdf.php 
