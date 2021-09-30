### Leetcode 61. [Rotate List](https://leetcode.com/problems/rotate-list/)

Given the head of a linked list, rotate the list to the right by k places.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

Input: head = [1,2,3,4,5], k = 2\
Output: [4,5,1,2,3]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

Input: head = [0,1,2], k = 4\
Output: [2,0,1]
 

**Constraints:**

- The number of nodes in the list is in the range [0, 500].
- -100 <= Node.val <= 100
- 0 <= k <= 2 * 10<sup>9</sup>
 
******************************
**Explanation**
- Base case is when the linked list has no node or 1 node.
- Traverse the linked list and get its length ```l``` and its last element ```oldTail```.
- The newTail is the ```(l - k % l - 1)th``` node.
- The newHead is the ```(l - k % l)th``` node.
- Break the link between newTail and newHead and link the oldTail to head to get the new linked list. 

**Python**

```python
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:        
        # base case
        if not head or not head.next:
            return head
        
        oldTail = head
        l = 1
        while oldTail.next:
            oldTail = oldTail.next
            l += 1
        oldTail.next = head
        
        # new tail: l - k % l - 1
        # new head: l - k % l         
        newTail = head
        for i in range(l - k % l - 1):
            newTail = newTail.next
        
        newHead = newTail.next
        newTail.next = None
        
        return newHead
```

**Complexity**

- Time Complexity: ```O(N)``` 
- Space Complexity: ```O(1)``` 
