## 题目：linkedin高频:Reservoir sampling
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/484.png)

https://www.geeksforgeeks.org/reservoir-sampling/

Reservoir sampling is a family of randomized algorithms for randomly choosing k samples from a list of n items, where n is either a very large or unknown number. Typically n is large enough that the list doesn’t fit into main memory. For example, a list of search queries in Google and Facebook.
So we are given a big array (or stream) of numbers (to simplify), and we need to write an efficient function to randomly select k numbers where 1 <= k <= n. Let the input array be stream[]. 

A simple solution is to create an array reservoir[] of maximum size k. One by one randomly select an item from stream[0..n-1]. If the selected item is not previously selected, then put it in reservoir[]. To check if an item is previously selected or not, we need to search the item in reservoir[]. The time complexity of this algorithm will be O(k^2). This can be costly if k is big. Also, this is not efficient if the input is in the form of a stream. 

It can be solved in O(n) time. 
The solution also suits well for input in the form of stream. The idea is similar to this post. Following are the steps.
1) Create an array reservoir[0..k-1] and copy first k items of stream[] to it. 
2) Now one by one consider all items from (k+1)th item to nth item. 
…a) Generate a random number from 0 to i where i is the index of the current item in stream[]. Let the generated random number is j. 
…b) If j is in range 0 to k-1, replace reservoir[j] with stream[i]

Following is the implementation of the above algorithm. 
# 类似 382&398
## 答案：
**答案**
```python
# to randomly select k items
# from a stream of items
import random
# # A utility function to print an array
# def printArray(stream,n):
#     for i in range(n):
#         print(stream[i],end=" ");
#     print();
 
# A function to randomly select  k items from stream[0..n-1].
def selectKItems(stream, n, k):
        i = 0
        # index for elementsin stream[]
         
        # reservoir[] is the output array. 
        #Initialize it with first k elements from stream[]
        reservoir = [0] * k
        for i in range(k):
            reservoir[i] = stream[i]
         
        # Iterate from the (k+1)th element to nth element
        while(i < n):
            # Pick a random index from 0 to i.
            j = random.randrange(i+1) #[a, b)这里[0, i+ 1）即[0, i]
#            j = random.randint(0, i) ##[a, b]
             
            # If the randomly picked index is smaller than k,
            # then replace the element present at the index
            # with new element from stream
            if(j < k):
                reservoir[j] = stream[i]
            i+=1;
         
        print("Following are k randomly selected items")
#         print(reservoir)
        printArray(reservoir, k)
     
# Driver Code
if __name__ == "__main__":
    stream = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
    n = len(stream);
    k = 5;
    selectKItems(stream, n, k)
```
## 思路：
https://leetcode.cn/problems/linked-list-random-node/solution/xu-shui-chi-chou-yang-suan-fa-by-idouble-g7y9/
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/485.png)

## 证明：

https://zhuanlan.zhihu.com/p/107889958

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/487.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/486.png)

