### Leetcode 513. [Find Bottom Left Tree Value](https://leetcode.com/problems/find-bottom-left-tree-value/)

Given the root of a binary tree, return the leftmost value in the last row of the tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/14/tree1.jpg) 

Input: root = [2,1,3]、
Output: 1

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/14/tree2.jpg) 

Input: root = [1,2,3,4,null,5,6,null,null,7]、
Output: 7

**Constraints:**

- The number of nodes in the tree is in the range [1, 104].
- 2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1

******************************
**Explanation**
- traverse the tree using BFS and queue
- store the first element at each level each time
- return the last first element
  
**Python**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        queue = [root]
        while queue:
            length = len(queue)
            res = queue[0].val
            for i in range(length):
                curr = queue.pop(0)
                if curr:
                    if curr.left:
                        queue.append(curr.left)
                    if curr.right:
                        queue.append(curr.right)
        return res      
```

**Complexity**

- Time Complexity: ```O(N)```
- Space Complexity: ```O(H)``` where H is the height of the tree
