## 题目：208. Implement Trie (Prefix Tree)

https://leetcode.com/problems/implement-trie-prefix-tree/

A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

Trie() Initializes the trie object.
void insert(String word) Inserts the string word into the trie.
boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.
 
```
Example 1:

Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
 

Constraints:

1 <= word.length, prefix.length <= 2000
word and prefix consist only of lowercase English letters.
At most 3 * 104 calls in total will be made to insert, search, and startsWith.
```
## 答案：

**方法一 plus dict(少写一个class)**
```python
#时间复杂度：初始化为 O(1)，其余操作为 O(|S|)，其中 |S| 是每次插入或查询的字符串的长度。
#空间复杂度：O(∣T∣)，其中 |T| 为所有插入字符串的长度之和

#对于每个节点都是一个字典dict， 它的键为后续的字符，值为这个字符对应的字典，
#同时对单词结尾的字符，我们添加一个键-1，如果-1在这个字典中，说明这个单词存在。
#整个结构相当于一层一层嵌套的字典，所以叫字典树。

class Trie:
    def __init__(self):
        #初始化根节点
        self.root = dict()
        
    def insert(self, word: str) -> None:
        cur = self.root
        for w in word:
            # 依次查找每个字符
            #如果w已经存在cur的键中了，说明w已经为cur的后续字符了，pass
            #不存在，则对字符cur创建一个字典，这个字典作为cur中w对应的值
            if w not in cur:
                cur[w] = dict()
            cur = cur[w]
        #单词最后一个字符的单词，加一个键-1，对应值存不存在都无所谓，只要-1这个键存在
        #就代表是单词结尾
        cur[-1] = True

    def search(self, word: str) -> bool:
        cur = self.root
        #开始遍历
        for w in word:
            if w in cur:
                cur = cur[w]
            #如果路上不存在这个字符，直接Fasle
            else:
                return False
        #遍历到最后，还需要看-1存不存在
        if -1 in cur:
            return True
        else:
            return False
       

    def startsWith(self, prefix: str) -> bool:
        #与上面search一样，只不过不需要看最后是不是True
        cur = self.root
        #开始遍历
        for w in prefix:
            if w in cur:
                cur = cur[w]
            #如果路上不存在这个字符，直接Fasle
            else:
                return False
        return True


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
**方法一dict**
```python
#时间复杂度：初始化为 O(1)，其余操作为 O(|S|)，其中 |S| 是每次插入或查询的字符串的长度。
#空间复杂度：O(∣T∣)，其中 |T| 为所有插入字符串的长度之和

##对于每个节点都是一个字典dict， 它的键为后续的字符，值为这个字符对应的字典，
##整个结构相当于一层一层嵌套的字典，所以叫字典树。

class Trie:
    def __init__(self):
        #初始化根节点
        self.root = TrieNode()
        
    def insert(self, word: str) -> None:
        cur = self.root
        for w in word:
            # 依次查找每个字符
            #如果w已经存在cur的键中了，说明w已经为cur的后续字符了，pass
            #不存在，则对字符cur创建一个字典，这个字典作为cur中w对应的值
            if w not in cur.next:
                cur.next[w] = TrieNode()
            cur = cur.next[w]
        #单词最后一个字符的单词，加一个键-1，对应值存不存在都无所谓，只要-1这个键存在
        #就代表是单词结尾
        cur.is_word = True

    def search(self, word: str) -> bool:
        cur = self.root
        #开始遍历
        for w in word:
            cur = cur.next.get(w)
            if cur is None:
            #如果路上不存在这个字符，直接Fasle
                return False
        # 如果每个字符都有且是完整单词，才说明查找单词成功
        return cur.is_word
       

    def startsWith(self, prefix: str) -> bool:
        #与上面search一样，只不过不需要看最后是不是True
        cur = self.root
        #开始遍历
        for w in prefix:
            cur = cur.next.get(w)
            if cur is None:
            #如果路上不存在这个字符，直接Fasle
                return False
        return True
class TrieNode:
    def __init__(self):
        self.next = {}
        self.is_word = False
# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)

```
**方法二plus ：数组(少写一个class)**
```python

#时间复杂度：初始化为 O(1)，其余操作为 O(|S|)，其中 |S| 是每次插入或查询的字符串的长度。
#空间复杂度：O(∣T∣⋅Σ)，其中 |T| 为所有插入字符串的长度之和，Σ 为字符集的大小，本题 Σ=26。
class Trie:
    
    def __init__(self):
        """
        Initialize your data structure here.
        """
        #不同！！！
        self.next = [None] * 26 
        self.is_word = False


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        cur = self #   #不同！！！
        for w in word:
            # 依次查找每个字符
            # 如果所有下一个结点中没有当前字符，则增加新结点到下一个next[idx]
            idx = ord(w) - ord('a')
            if cur.next[idx] == None:
                cur.next[idx] = Trie() #不同！！！
            cur = cur.next[idx]
        # 把最后一个字符对应的is_word(val)置为True，表示为单词的结束
        cur.is_word = True
        
    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        cur = self #不同！！！
        for w in word:
            idx = ord(w) - ord('a')
            # 如果有下一个对应字符的结点，那么继续查找下一个结点
            # 如果没有下一个对应字符的结点，那么说明查找单词失败
            if cur.next[idx] != None:
                cur = cur.next[idx]
            else: 
                return False
        # 如果每个字符都有且是完整单词，才说明查找单词成功
        return cur.is_word

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        #与上面search一样，只不过不需要看最后是不是True
        cur = self #不同！！！
        for w in prefix:
            idx = ord(w) - ord('a')
            # 如果有下一个对应字符的结点，那么继续查找下一个结点
            # 如果没有下一个对应字符的结点，那么说明查找单词失败
            if cur.next[idx] != None:
                cur = cur.next[idx]
            else: 
                return False
        return True
        
# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)

```
**方法二 数组**
```python
#时间复杂度：初始化为 O(1)，其余操作为 O(|S|)，其中 |S| 是每次插入或查询的字符串的长度。
#空间复杂度：O(∣T∣⋅Σ)，其中 |T| 为所有插入字符串的长度之和，Σ 为字符集的大小，本题 Σ=26。

#https://www.pythonf.cn/read/123752
class Trie:
    
    def __init__(self):
        """
        Initialize your data structure here.
        """
        #初始化根节点
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        cur = self.root
        for w in word:
            # 依次查找每个字符
            # 如果所有下一个结点中没有当前字符，则增加新结点到下一个next[idx]
            idx = ord(w) - ord('a')
            if cur.next[idx] == None:
                cur.next[idx] = TrieNode()
            cur = cur.next[idx]
        # 把最后一个字符对应的is_word(val)置为True，表示为单词的结束
        cur.is_word = True
        
    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        cur = self.root
        for w in word:
            idx = ord(w) - ord('a')
            # 如果有下一个对应字符的结点，那么继续查找下一个结点
            # 如果没有下一个对应字符的结点，那么说明查找单词失败
            if cur.next[idx] != None:
                cur = cur.next[idx]
            else: 
                return False
        # 如果每个字符都有且是完整单词，才说明查找单词成功
        return cur.is_word

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        #与上面search一样，只不过不需要看最后是不是True
        cur = self.root
        for w in prefix:
            idx = ord(w) - ord('a')
            # 如果有下一个对应字符的结点，那么继续查找下一个结点
            # 如果没有下一个对应字符的结点，那么说明查找单词失败
            if cur.next[idx] != None:
                cur = cur.next[idx]
            else: 
                return False
        return True
#######
##定义Trie节点，is_word(val)表示这个结点为止是不是一个单词，
###next表示这个节点之后的字符的树节点数组，长度为26，表示a-z，
###初始化为没有后续字符，所以都为None
class TrieNode:
    def __init__(self):
        self.is_word = False
        self.next = [None] * 26 

        
# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```


## 思路：

### dict：定义class TrieNode()
```
#时间复杂度：初始化为 O(1)，其余操作为 O(|S|)，其中 |S| 是每次插入或查询的字符串的长度。

#空间复杂度：O(∣T∣)，其中 |T| 为所有插入字符串的长度之和

##定义Trie节点，is_word(val)表示这个结点为止是不是一个单词，
##next表示这个节点之后的字符的树节点用dict
```
**方法一plus dict(少写一个class)**

#https://leetcode.cn/problems/implement-trie-prefix-tree/solution/fu-xue-ming-zhu-cong-er-cha-shu-shuo-qi-628gs/
```
##对于每个节点都是一个字典dict， 它的键为后续的字符，值为这个字符对应的字典，
##同时对单词结尾的字符，我们添加一个键-1，如果-1在这个字典中，说明这个单词存在。
##整个结构相当于一层一层嵌套的字典，所以叫字典树。
```

**方法一 dict**

https://leetcode.cn/problems/implement-trie-prefix-tree/solution/fu-xue-ming-zhu-cong-er-cha-shu-shuo-qi-628gs/
```
##对于每个节点都是一个字典dict， 它的键为后续的字符，值为这个字符对应的字典，

##整个结构相当于一层一层嵌套的字典，所以叫字典树。
```
### 数组：定义class TrieNode()**

#时间复杂度：初始化为 O(1)，其余操作为 O(|S|)，其中 |S| 是每次插入或查询的字符串的长度。

#空间复杂度：O(∣T∣⋅Σ)，其中 |T| 为所有插入字符串的长度之和，Σ 为字符集的大小，本题 Σ=26。
```
##定义Trie节点，is_word(val)表示这个结点为止是不是一个单词，
###next表示这个节点之后的字符的树节点数组，长度为26，表示a-z，
###初始化为没有后续字符，所以都为None`
```

**方法二 plus 数组(少写一个class)**
```
#那么Trie树中，我们首先定义一个root节点，然后在insert操作中，不断根据下面一个结点是什么字母，
#根据ASCII码算数组的下标，定义一个新的TrieNode，来更新next数组，
#单词的最后一个字符对应的TrieNode结点的val置为True，表示是一个单词的结尾。
```

**方法二 数组**
https://www.pythonf.cn/read/123752
```
#那么Trie树中，我们首先定义一个root节点，然后在insert操作中，不断根据下面一个结点是什么字母，
#根据ASCII码算数组的下标，定义一个新的TrieNode，来更新next数组，
#单词的最后一个字符对应的TrieNode结点的val置为True，表示是一个单词的结尾。
```


![a](https://github.com/SSRRBB/Leetcode/blob/main/Images/453.png)
