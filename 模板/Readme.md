## 0.Math
- **263, 204**

## 00.Intuitive or Greedy
- **277, 997**
- **56**

## 1. 数组/列表（list）
- **同向双指针快慢指针**(移除元素)
```
(27,26,80; 283,844)
```
- **同向双指针sliding window**(解决一些连续问题substring&subarray是连续的；subsequence是不连续的)
```
209(非固定窗口) 643（固定窗口）
非固+哈希表 3,340, 159=904-》992（atMost变）; 487, 1004,1695
固+ 两个哈希 438，567，76；
非固：1208
固+ 变通： 1052，1423，1151
485 特殊 不用sliding
1819lint(特别)
大号：1248（类似 992）；1348（类似992 atleast）;1234(76)

3&159&209&1695&438&567&487&1004&1208&1052&1423&1151


```
https://github.com/azl397985856/leetcode/blob/master/thinkings/slide-window.md

https://leetcode.com/problems/binary-subarrays-with-sum/discuss/186683/
- **相向双指针Two sum型**（167sorted模板）
```
(167, 1, 170)(15,18, 16）(1099，609lin,443lin-> 611,259)
(977)
(11，42？)

```
- **相向双指针 partition，空间0（1）** （31lin模板）
```
905 & 49(lin);144(lin)&922；75&143(lint);215
（88，493）
（21，148 链表）
```
- **二分法** 704&34(模板)详细看下面

- **模拟法**（螺旋矩阵)(59,54)

## 2. 字符串(str)

- **ASCII:Palindrome**(1781(lin), 1784(lin),958(lin))

- **相向双指针Reverse**（**list与str怎么相互转换**）

  - ***反转字符串***（34，542，151，557，186，58(jian)）
  - ***判断回文子串***(125， 860）

- **同向双指sliding window** 1819(特别)，其他参考 1.数组

- **28，459？？？**


## 3.链表（203，237，219(lin)删除插入模板）
```diff
+ 反转链表
+ 快慢指针，就这两类
```
- **Design 707(?)**
- **反转 206,92，234，24，25**
- **同向快慢指针，链表环 141,142,202**
- **同向双指针快慢指针 (19求链表长度,1721根据n)(876两倍速度)（328）**
- **快慢61，160**
- **math 2**
- **21，23 (?)**
- **148(21 + 876)**
- **19,160还给了怎么求链表长度**


## 1A.双指针two pointer(算法之王) 0（n）
- **数组，字符串和链表都有涉及**

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/250.png)

## 1AA. **快速排序O(nlgon)-O(n^2)空间0(logn)-O(n); 归并排序O(nlgon)-O(n^2)空间O(n)（912）**
- **912**
- **88,493；21,148**
- **相向双指针 partition**

## 1AAA.**前缀和**（subarray可以用sliding window或者前缀和）
- **1480,303,304模板**
- **724；(1475lin, 325, 1844lin）；643**
- **560 ==930 小模板，1248，974,523**

https://github.com/azl397985856/leetcode/blob/master/selected/atMostK.md

https://leetcode-cn.com/problems/count-number-of-nice-subarrays/solution/de-liao-wo-ba-qian-zhui-he-gei-ba-de-gan-ymzz/

https://leetcode-cn.com/problems/subarray-sums-divisible-by-k/solution/xiong-mao-shua-ti-python3-you-qian-zhui-he-fu-xi-p/

## 2B. 二分法 O(logn)

https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/

```diff
+ 用 start + 1 < end的目的是为了避免死循环
+ 时间复杂度低，O(logn)
+ 寻找峰值或者连绵山峰（画图寻找）
```

- **在有序数据集上,二分求下标**
```
(一个数组00XX,找数组中第一个/最后一个满足某个条件的位置 OO...OOXX....XX) 704&34(模板),35
540(corner case太多了); 658(heap)
```
- **在未排序数据集上,局部单调性，二分求下标**
```
(找到条件，形成00XX) 旋转数组rotate array、 山峰/（画图）:153(154),33(81)，1095（多次二分）；852（简单山峰）
(无法找到一个条件，形成 XXOO 的模型 但可以根据判断，保留下有解的那一半或者去掉无解的一半),162（连绵山峰）, 1091（matrix）（162延伸）,74,240都是matrix
```

- **在答案上(在一个有范围的区间里搜索一个整数)**
```
69,&367；278== 374,278 = 374(API); 702(倍增,API)； 287（精彩）
```
- **在答案集上**
```
(求满足某条件的最大值或者最小值,最终结果是个有限的集合,每个结果有一个对应的映射,结果集合跟映射集合正相关或着负相关
,可以通过在映射集合上进行二分，从而实现对结果集合的二分) 
875; 410,1101
```

## 4.哈希表
- **Two sum, four sum (1,167,170)(454,532)**
- **Design 705, 706???**
- 
- **26个字母既可以是数组模拟dict,也可以直接建立dict: 242,383,49 anagram，249(defaultdict)**
- **[数字]:349,350,1213 ->[字符串]：2085，884， 2053 -> [字符串>字符]：1002**
- **同向快慢指针，链表环 141,142,202**
- 
- **前缀和(1475lin, 325, 1844lin）(560)**
-
- **First Unique (387, 685lint)**
- **data stream (960lint, 1429, 146LRU, 460,LFU, 380)**
-
- - **signle number 136,137 bit manipulation**
- **734,781**

## 5.栈 and 队列
- **492,232,225 知识点 (281, 346, 362)**
- **232，20**
- 
## 6.堆
Top K 问题
- **离线 973,347,215,658,2654**
- **在线 703，295，23**



![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/253.png)

## 3C.BFS

- **基于树的BFS（分层遍历，最短路径)**
```
102模板429(Ntree)
103+（10道题)(107,199,637,515,116,117,513)
314（哈希表）;662
104,22,559,111(detpth) DFS/BFS都可以； 110（height）DFS
BFS/DFS（297，428序列化）更好的理解BFS/DFS
```
- **基于图的BFS（分层遍历，连通块问题,最短路径**
```
133模板（遍历）,127,863
200模板（连通块), 1197
542或者1730模板(最短路经)，1162，1293
```

- **拓扑排序**
```
207,210(模板)
444
269?
```

## 4C.DFS
```diff
- 二叉树的分治本质是做后序遍历;所以我们好多题其实是DFS后序遍历(从下到上)
- 分治是特殊的遍历；
+ 二叉树是天然的分治结构；

```

```diff
- 二叉搜索树(BST):左子树节点的值<根节点的值，右子树节点的值>=根节点的值
- 相等情况的点可能在右子树，也可能在左子树，需要跟面试官澄清
+ 中序遍历结果有序（不下降的顺序，有些临点可能相等）
- 如果二叉树的中序遍历不是不下降序列，则一定不是BST
- 如果二叉树的中序遍历是不下降，也未必是BST
+ BST的高度：最好O(n);最坏o(logN);用o(h)表示更合适
```
**DFS的recursion与iteration写法**

**中序遍历的iteration写法要会**

**144，94，145&589，590（Ntree)**

- **二叉树的分治和遍历（BFS/DFS）**
   - ***二叉树上求值/路径 BFS/DFS（297，428序列化）(104,222,559,111,BFS/DFS)(110 DFS)( 两个点或树DFS/BFS：101,100,572dfs,617前序;1120&586(lint)DFS)（leaves404，481(lint)，872DFS，366SFS）(250)***
   - ***二叉树上求路径 （路径path 124&543 DFS,257, 113, 112,437回溯）(lca 236,1644,1650)***
   - ***二叉树结构变化(226BFS/DFS) （递归 114，105，106，654）***
   - ***BST:(700,235),(98,530,501,538，173)(递归好晕701，450，669，108,538)*** 
- **在已知图树上遍历**

## 5D 回溯
- **求子集组合排列**
```diff
+ 找点自动回溯，找路径手动回溯
```
```
上面path 题目也有点回溯的感觉
路径path 124&543 DFS,257, 113, 112,437回溯
```
 - ***78子集；90 77组合； 46排列


## 6F.动态规划DQ

![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/286.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/377.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/378.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/379.png)
![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/380.png)
