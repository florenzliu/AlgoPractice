### Leetcode 109. [Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

![](https://assets.leetcode.com/uploads/2020/08/17/linked.jpg) 

**Example 1:**


Input: head = [-10,-3,0,5,9]\
Output: [0,-3,9,-10,null,5]\
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.

**Example 2:**

Input: head = []\
Output: []

**Example 3:**

Input: head = [0]\
Output: [0]

**Example 4:**

Input: head = [1,3]\
Output: [3,1]
 

**Constraints:**

- The number of nodes in head is in the range [0, 2 * 104].
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup> 
******************************
**Explanation**
- Iterate over the linked list to find its length
- Simulate the inorder traversal by using the mid point, i.e. (start + end) / 2.
- Recurse on the left half, process the current head value, progress the head node to the next node, and then recurse on the right half.

**Python**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        # inorder simulation
        # find size
        size = 0
        curr = head
        while curr:
            size += 1
            curr = curr.next
            
        def helper(start, end):   
            nonlocal head
            if start > end:
                return None
            mid = (start + end) // 2
            left = helper(start, mid-1)
            
            node = TreeNode(head.val)
            node.left = left
            
            head = head.next
            
            right = helper(mid+1, end)
            node.right = right
            
            return node
        
        return helper(0, size-1)
```

**Complexity**

- Time Complexity: ```O(N)``` where ```N``` is the size of the linked list
- Space Complexity: ```O(logN)``` since the height of the height-balanced BST is bounded by logN
