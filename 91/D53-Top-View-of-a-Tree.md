### [Top View of a Tree](https://binarysearch.com/problems/Top-View-of-a-Tree)
Given a binary tree root, return the top view of the tree, sorted left-to-right.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)
```
Input: root = [1, [2, null, [4, null, [5, null, [6, null, [7, null, null]]]]], [3, null, null]]
Output: [2, 1, 3, 6, 7]
Explanation:
Note that directly above 4 is 1 and directly above 5 is 3 so these are not part of the top view.
```

**Example 2:**

```
Input: root = [3, [1, [0, null, null], [2, null, null]], [4, null, null]]
Output: [0, 1, 3, 4]
```

**Constraints:**

- n ≤ 100,000 where n is the number of nodes in root

******************************
**Explanation**
- bfs
- use x to keep track of the position of the node vertically
- use a hashmap to store the first element in the vertical column

**Python**

```python
# class Tree:
#     def __init__(self, val, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def solve(self, root):
        res = {}

        queue = [(root, 0)]
        while queue:
            for i in range(len(queue)):
                node, x = queue.pop(0)
                if x not in res:
                    res[x] = node.val
                if node.left:
                    queue.append((node.left, x-1))
                if node.right:
                    queue.append((node.right, x+1))
        
        ans = []
        for i in sorted(res.keys()):
            ans.append(res[i])
        
        return ans
```

**Complexity**:

- Time Complexity: ```O(nlogn)``` (this can be improved to n by using min value of keys)
- Space Complexity: ```O(n)```
