### Leetcode 494. [Target Sum](https://leetcode.com/problems/partition-equal-subset-sum/)
Given a non-empty array nums containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Example 1:**

```
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**

```
Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.
```

**Constraints:**

- 1 <= nums.length <= 200
- 1 <= nums[i] <= 100
- 
******************************
**Explanation**
- math problem (since nums is a list of non-negative numbers): 
  - positive + negative = target
  - positive - negative = total
  - => positive = (target+total)/2
- knapsack problem using 1-D dp: the number of knapsack is positive
  - dp[i] = dp[i-nums[j]]

**Python**

```python
class Solution:
    # Approach 1: backtracking
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        @lru_cache(None)
        def backtracking(n, currSum):
            if n < 0:
                if currSum == 0: 
                    return 1
                return 0
            return backtracking(n-1, currSum - nums[n]) + backtracking(n-1, currSum + nums[n])
                   
        return backtracking(len(nums)-1, target)
    
    # Approach 2: bottom up dynamic programming (knapsack)
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        if (target + sum(nums)) % 2 or sum(nums) < abs(target):
            return 0
        positive = (target + sum(nums)) // 2
        dp = [0 for i in range(positive+1)]
        dp[0] = 1
        
        for i in range(len(nums)):
            for j in range(positive, nums[i]-1, -1):
                dp[j] += dp[j-nums[i]]
        return dp[-1]
        
```

**Complexity**:

- Time Complexity: ```O(mn)``` where m is (total+target)//2 and n is the length of the nums list
- Space Complexity: ```O(m)```
