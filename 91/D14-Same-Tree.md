### Leetcode 100. [Same Tree](https://leetcode.com/problems/same-tree/)

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg) 

Input: p = [1,2,3], q = [1,2,3]\
Output: true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg) 

Input: p = [1,2], q = [1,null,2]\
Output: false

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg) 

Input: p = [1,2,1], q = [1,1,2]
Output: false

**Constraints:**

- The number of nodes in both trees is in the range [0, 100].
- -10<sup>4</sup> <= Node.val <= 10<sup>4</sup>

******************************
**Explanation**
- Approach 1: recursion
  - Traverse the tree and check if the current node exists and the values of the current node are equal during the traversal
  - Then check the left child and the right child
- Approach 2: iteration
  - use a queue and BFS to traverse each level
  - the queue element is a pair of current node in p and q

**Python**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

# Approach 1
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not p and not q:
            return True
        if not p or not q:
            return False
        if p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
    
# Approach 2
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        def isSameNode(a, b):
            if not a and not b:
                return True
            if not a or not b:
                return False
            return a.val == b.val
        
        queue = [(p,q)]
        while queue:
            p, q = queue.pop(0)
            if not isSameNode(p,q):
                return False
            if p:
                queue.append((p.left, q.left))
                queue.append((p.right, q.right))
        return True          
```

**Complexity**

- Time Complexity: ```O(N)```
- Space Complexity: ```O(N)``` in the worst case and ```O(logN)``` in the best case