### Leetcode 876. [ Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)
```
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)
```
Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
```

**Constraints:**

- The number of nodes in the list is in the range [1, 100].
- 1 <= Node.val <= 100

******************************
**Explanation**
- use two pointers: fast and slow
- at each round, slow pointer moves 1 step, fast pointer moves 2 steps
- when fast pointer reached the end of the linked list, stop and return the slow pointer

**Python**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        slow, fast = head, head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
        return slow
```

**Complexity**:

- Time Complexity: ```O(n)```
- Space Complexity: ```O(1)```
