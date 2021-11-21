### Leetcode 96. [Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)
```
Input: n = 3
Output: 5
```

**Example 2:**

```
Input: n = 1
Output: 1
```

**Constraints:**

- 1 <= n <= 19

******************************
**Explanation**
- greedy approach: sort the array people by its weight first
  - at most two persons: we can use two pointers, put the current lightest and the current heaviest in the remaining people on the same boat
  - if the sum is larger than the limit, put the heaviest alone in a boat, move to the next heaviest one
  - otherwise, move to the next lightest and the next heaviest
  
**Python**

```python
class Solution:
    def numRescueBoats(self, people: List[int], limit: int) -> int:
        people.sort()
        i, j = 0, len(people)-1
        
        count = 0
        while i <= j:
            if people[i] + people[j] <= limit:
                i += 1
            count += 1
            j -= 1
        return count  
```

**Complexity**:

- Time Complexity: ```O(nlogn)```
- Space Complexity: ```O(1)```
