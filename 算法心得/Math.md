## reminder
```
python是向下整除，不是向零整除：

10 // -3 = -4
-10 // -3 = -4

**10 % -3 = -2** 怎么怎么计算出来的呢?  x % y 等价于 x - (x // y)y


10 % -3 = -2 = 10 - (-4)(-3) = 10 - 12 = -2
7 % - 4 = -1  (同理)

-10 % 3 =  2 = -10 - (-4)*3 = -10 + 12 
-7 % 4 = 1   

(7% - 4 = 3 java)
(-7%4= -3 java)   
```

## random
**闭区间是bounded interval; 开区间是unbounded interval;**
```
import numpy as np
import random

random.randint(1, 5)  生成[1, 5]之间的一个整数

np.random.randint(1, 5)   生成[1, 5)之间的一个整数

random.random() 	生成一个 [0,1) 之间的均匀分布浮点数

```


## Division in math
```
A ➗ B = C……D 
dividend ➗divisor = quotient……remainder
numerator  denominator

被除数➗除数=商……余数
分子分母

A over B
A by B
A divided by B
B divides A

A is divisible by B: Remainder D is 0
A 能被 B 整除(12 is sivisible by 4)
12 % 4 -> 0
```

## Prime
- A **prime number质数** is a number greater than 1 with only two factors – themselves and 1.

- **Composite numbers** are whole numbers that have two factors and are not prime numbers, as they can be divided by more than two numbers

- **Prime factor质因数** is the factor of the given number which is a prime number. 

- **Prime factorization质因数分解** is a way of expressing a number as a product of its prime factors

-**Factors因数** are the numbers you multiply together to get another number



