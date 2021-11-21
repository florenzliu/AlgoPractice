### Leetcode 677. [Map Sum Pairs](https://leetcode.com/problems/map-sum-pairs/)
Design a map that allows you to do the following:

- Maps a string key to a given value.
- Returns the sum of the values that have a key with a prefix equal to a given string.

Implement the MapSum class:

- MapSum() Initializes the MapSum object.
- void insert(String key, int val) Inserts the key-val pair into the map. If the key already existed, the original key-value pair will be overridden to the new one.
- int sum(string prefix) Returns the sum of all the pairs' value whose key starts with the prefix.

**Example 1:**

```
Input
["MapSum", "insert", "sum", "insert", "sum"]
[[], ["apple", 3], ["ap"], ["app", 2], ["ap"]]
Output
[null, null, 3, null, 5]

Explanation
MapSum mapSum = new MapSum();
mapSum.insert("apple", 3);  
mapSum.sum("ap");           // return 3 (apple = 3)
mapSum.insert("app", 2);    
mapSum.sum("ap");           // return 5 (apple + app = 3 + 2 = 5)
```


**Constraints:**

- 1 <= key.length, prefix.length <= 50
- key and prefix consist of only lowercase English letters.
- 1 <= val <= 1000
- At most 50 calls will be made to insert and sum.

******************************
**Explanation**

For TrieNode:
- presum: the sum of the values whose keys have the same prefix till the current TrieNode 
- children: a dictionary

For Trie:
- root: the root of a tree
- map: a hashmap of key-value pair

**Python**

```python
class TrieNode:
    def __init__(self):
        self.presum = 0
        self.children = {}
    
class MapSum:

    def __init__(self):
        self.map = {}
        self.root = TrieNode()

    def insert(self, key: str, val: int) -> None:
        delta = val - self.map[key] if key in self.map else val
        self.map[key] = val
        node = self.root

        for ch in key:
            if ch not in node.children:
                node.children[ch] = TrieNode()
            node.children[ch].presum += delta
            node = node.children[ch]        
        
    def sum(self, prefix: str) -> int:
        node = self.root
        for ch in prefix:
            if ch not in node.children:
                return 0
            node = node.children[ch]
        return node.presum

# Your MapSum object will be instantiated and called as such:
# obj = MapSum()
# obj.insert(key,val)
# param_2 = obj.sum(prefix)
```

**Complexity**:

- Time Complexity: ```O(K)``` where K is the length of the key
- Space Complexity: ```O(n)``` where n is the size of the total input
