### Leetcode 416. [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)
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
- equal to find a subset with sum of sum(nums) // 2
- top down approach using dfs + memoization
- bottom up approach using 2-D dp[i][j]: true if the sum j can be formed by array elements in the subset nums[0] ~ nums[i]
  - dp[i][j] = dp[i-1][j] or dp[i-1][j-nums[i]]
- improve space complexity using 1-D dp[i]: true if the sum i can be formed
  - dp[i] = dp[i] or dp[i-currNum]

**Python**

```python
class Solution:
    # Approach 1: top down dynamic programming
    def canPartition(self, nums: List[int]) -> bool:
        if sum(nums) % 2:
            return False
        target = sum(nums) // 2
        @lru_cache(maxsize=None)
        def dfs(n, currSum):
            if currSum < 0 or n < 0:
                return False
            if currSum == 0:
                return True
            return dfs(n-1, currSum) or dfs(n-1, currSum-nums[n])
        return dfs(len(nums)-1, target)
    
    # Approach 2: bottom up dynamic programming
    def canPartition(self, nums: List[int]) -> bool:
        if sum(nums) % 2:
            return False
        target = sum(nums) // 2
        dp = [[0 for _ in range(target+1)] for _ in range(len(nums)+1)]
        dp[0][0] = 1

        for i in range(1, len(nums)+1):
            for j in range(target+1):
                if j < nums[i-1]:
                    dp[i][j] = dp[i-1][j]
                else:
                    dp[i][j] = dp[i-1][j] or dp[i-1][j-nums[i-1]]
        return dp[-1][target]
    
    # Approach 3: 1d dynamic programming
        if sum(nums) % 2:
            return False
        target = sum(nums) // 2
        dp = [0 for _ in range(target+1)]
        dp[0] = 1
        for n in nums:
            for i in range(target, n-1, -1):
                dp[i] = dp[i] or dp[i-n]
        return dp[-1]        
```

**Complexity**:

- Time Complexity: ```O(mn)``` where m is the length of nums list and n is the subsetSum, i.e., total_sum / 2
- Space Complexity: ```O(mn) or O(n)```
