### Leetcode 129. [Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

You are given the root of a binary tree containing digits from 0 to 9 only.

Each root-to-leaf path in the tree represents a number.

- For example, the root-to-leaf path 1 -> 2 -> 3 represents the number 123.

Return the total sum of all root-to-leaf numbers. Test cases are generated so that the answer will fit in a 32-bit integer.

A leaf node is a node with no children.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg) 

Input: root = [1,2,3]\
Output: 25\
Explanation:\
The root-to-leaf path 1->2 represents the number 12.\
The root-to-leaf path 1->3 represents the number 13.\
Therefore, sum = 12 + 13 = 25.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/num2tree.jpg) 

Input: root = [4,9,0,5,1]\
Output: 1026\
Explanation:\
The root-to-leaf path 4->9->5 represents the number 495.\
The root-to-leaf path 4->9->1 represents the number 491.\
The root-to-leaf path 4->0 represents the number 40.\
Therefore, sum = 495 + 491 + 40 = 1026.

**Constraints:**

- The number of nodes in the tree is in the range [1, 1000].
- 0 <= Node.val <= 9
- The depth of the tree will not exceed 10.

******************************
**Explanation**
- Approach 1: recursion
  - Write a helper function (node, currSum) to traverse the tree to find all the numbers from root to leaf
  - Update currSum at each node
  - When the node is leaf node, add currSum to the total sum
- Approach 2: iteration
  - Use a stack to store (node, currSum) at each node and DFS 
  - Update currSum at each node 
  - When the node is leaf node, add currSum to the total sum
  
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
    def sumNumbers(self, root: TreeNode) -> int:
        def helper(node, currSum):
            nonlocal s
            if node:
                currSum = currSum * 10 + node.val
                if not node.left and not node.right:
                    s += currSum
                helper(node.left, currSum)
                helper(node.right, currSum)
        s = 0
        helper(root, 0)
        return s
    
# Approach 2
class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        s = 0
        stack =[(root, 0)]
        while stack:
            node, currSum = stack.pop()
            if node:
                currSum = currSum * 10 + node.val
                if not node.left and not node.right:
                    s += currSum
                if node.left:
                    stack.append((node.left, currSum))
                if node.right:
                    stack.append((node.right, currSum))
        return s          
```

**Complexity**

- Time Complexity: ```O(N)```
- Space Complexity: ```O(H)``` where H is the height of the tree