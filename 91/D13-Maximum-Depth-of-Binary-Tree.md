### Leetcode 104. [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg) 

**Example 1:**


Input: root = [3,9,20,null,null,15,7]\
Output: 3

**Example 2:**

Input: root = [1,null,2]\
Output: 2

**Example 3:**

Input: root = []\
Output: 0

**Example 4:**

Input: root = [0]\
Output: 1
 

**Constraints:**

- The number of nodes in the tree is in the range [0, 10<sup>4</sup>].
- -100 <= Node.val <= 100

******************************
**Explanation**
- Approach 1: recursion
  - Traverse the tree and record the depth during the traversal
- Approach 2: iteration
  - Keep the next nodes to visit in a stack (dfs), which is the same order as the one in recursion

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
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1

# Approach 2
class Solution:
    def maxDepth(self, root: TreeNode) -> int: 
        stack = [(root,1)]
        maxDepth = 0
        while stack:
            node, depth = stack.pop()
            if node:
                maxDepth = max(maxDepth, depth)
                stack.append((node.left, depth+1))
                stack.append((node.right, depth+1))

        return maxDepth
```

**Complexity**

- Time Complexity: ```O(N)```
- Space Complexity: ```O(N)``` 