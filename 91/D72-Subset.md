### Leetcode 78. [Subset](https://leetcode.com/problems/subsets/)
Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

**Constraints:**

- 1 <= nums.length <= 10
- -10 <= nums[i] <= 10
- All the numbers of nums are unique.

******************************
**Explanation**
- approach 1: backtracking
- approach 2: bit manipulation

**Python**

```python
class Solution:
    # Approach 1: backtracking
    def subsets(self, nums: List[int]) -> List[List[int]]:
        def backtracking(curr, first):
            if len(curr) == k:
                result.append(curr[:])
                return
            
            for i in range(first, n):
                curr.append(nums[i])
                backtracking(curr, i+1)
                curr.pop()
            
        result = []
        n = len(nums)
        for k in range(n+1):
            backtracking([], 0)
        return result
    
    # Approach 2: bit manipulation
    def subsets(self, nums: List[int]) -> List[List[int]]:
        result = []
        end = 1 << len(nums)
        for sign in range(end):
            subset = []
            for i in range(len(nums)):
                print(i, 1 << i, sign, (1 << i) & sign)
                if ((1 << i) & sign) != 0:
                    subset.append(nums[i])
            result.append(subset)
        return result
```

**Complexity**:

- Time Complexity: ```O(n)```
- Space Complexity: ```O(1)```
