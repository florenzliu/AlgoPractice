### Leetcode 24. [Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg) 

**Example 1:**


Input: head = [1,2,3,4]\
Output: [2,1,4,3]

**Example 2:**

Input: head = []\
Output: []

**Example 3:**

Input: head = [1]\
Output: [1]
 

**Constraints:**

- The number of nodes in the list is in the range [0, 100].
- 0 <= Node.val <= 100
 
******************************
**Explanation**
- Break the linked list into pairs by jumping in steps of two.
- Swap the nodes by implementing ```prev``` and ```curr``` nodes: 
  - prev.next = curr.next
  - curr.next = curr.next.next
  - finally, prev.next.next = curr
- Update the ```prev``` and ```curr``` nodes to the next node pair

**Python**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        sentinel = ListNode()
        sentinel.next = head
        
        prev = sentinel
        curr = head
        while curr and curr.next:
            # swap the next 2 nodes
            prev.next = curr.next
            curr.next = curr.next.next
            prev.next.next = curr
            # update prev and curr nodes
            prev = curr
            curr = curr.next
        
        return sentinel.next
```

**Complexity**

- Time Complexity: ```O(N)``` where ```N``` is the size of the linked list
- Space Complexity: ```O(1)``` 
