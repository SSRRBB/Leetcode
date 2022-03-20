## 前缀和 （prefix sum）

- **这种通过记录数组前一部分的元素值来解题的思路，称为前缀和**
```
对于一个数组 nums,对应的前缀和pre
pre[0] = nums[0]
pre[1] = nums[0] + nums[1]

pre[i] = nums[0] + nums[1] + …… + nums[i]

如果我想要求A[i] + A[i+1] + ... + A[j]的值(0 <= i <= j <= n)
```
**i = 0 时比较麻烦**
- **pre[i] = nums[i] + pre[i - 1]**
- **nums[i]到nums[j]直接的和：pre[j] - pre[i = 1]**

**求 pre[i] = nums[0] + nums[1] + …… + nums[i]**
```python
nums = [3, 5, 2, -2, 4, 1]
pre = [0 for i in range(len(nums)]
for i in range(len(nums)):
    if i == 0:
        pre[i] = nums[i]
    else:
        pre[i] = nums[i] + pre[i - 1]
```

