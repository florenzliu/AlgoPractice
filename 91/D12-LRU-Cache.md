### Leetcode 146. [LRU Cache](https://leetcode.com/problems/lru-cache/)

Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:

- ```LRUCache(int capacity)``` Initialize the LRU cache with positive size capacity.
- ```int get(int key)``` Return the value of the key if the key exists, otherwise return -1.
- ```void put(int key, int value)``` Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key. 

The functions get and put must each run in O(1) average time complexity.

 

**Example 1:**

Input\
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]\
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]\
Output\
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation\
LRUCache lRUCache = new LRUCache(2);\
lRUCache.put(1, 1); // cache is {1=1}\
lRUCache.put(2, 2); // cache is {1=1, 2=2}\
lRUCache.get(1);    // return 1\
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}\
lRUCache.get(2);    // returns -1 (not found)\
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}\
lRUCache.get(1);    // return -1 (not found)\
lRUCache.get(3);    // return 3\
lRUCache.get(4);    // return 4
 

**Constraints:**

- 1 <= capacity <= 3000
- 0 <= key <= 10<sup>4</sup>
- 0 <= value <= 10<sup>5</sup>
- At most 2 * 10<sup>5</sup> calls will be made to get and put.


******************************
**Explanation**
- Approach 1: use OrderedDict() (a combination of hashmap and linked list) in Python
- Approach 2: use hashmap + double linked list
  - DLinkedList node has key, val, prev, next
  - LRUCache has capacity, size, head, tail, cache (hashmap)
    - always add node right after the head
    - put: first remove the node if exists, then add it right after the head, check if the length has exceeded the capacity, delete the tail.prev if size exceeded
    - get: first remove the node, then add it right after the head

**Python**

```python
class DLinkedList():
    def __init__(self):
        self.key = 0
        self.val = 0
        self.prev = None
        self.next = None

class LRUCache():

    def __init__(self, capacity):
        self.capacity = capacity
        self.size = 0
        self.cache = {}
        
        self.head, self.tail = DLinkedList(), DLinkedList()
        self.head.next = self.tail
        self.tail.prev = self.head

    def get(self, key):
        if key in self.cache:
            node = self.cache[key]
            self.remove_node(node)
            self.add_to_head(node)
            return node.val
        return - 1

    def put(self, key, value):
        if key in self.cache:
            node = self.cache[key]
            self.remove_node(node)
            self.add_to_head(node)
            node.val = value
        else:
            newNode = DLinkedList()
            newNode.val = value
            newNode.key = key
            self.add_to_head(newNode)
            self.cache[key] = newNode
            self.size += 1
            
            if self.size > self.capacity:
                tail = self.tail.prev
                del self.cache[tail.key]
                self.remove_node(self.tail.prev)
                self.size -= 1
    
    def remove_node(self, node):
        prev = node.prev
        nxt = node.next
        prev.next = nxt
        nxt.prev = prev
        
    def add_to_head(self, node):
        # always add the new node right after the head
        prev = self.head
        nxt = self.head.next
        
        node.prev = prev
        node.next = nxt
        
        prev.next = node
        nxt.prev = node
```

**Complexity**

- Time Complexity: ```O(1)``` for get and put
- Space Complexity: ```O(capacity)``` 