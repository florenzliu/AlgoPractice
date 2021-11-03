### Leetcode 673. [Number of Longest Increasing Subsequence](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)
Given an integer array nums, return the number of longest increasing subsequences.

Notice that the sequence has to be strictly increasing.

**Example 1:**

```
Input: nums = [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].
```

**Example 2:**

```
Input: nums = [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```

**Constraints:**

- 1 <= nums.length <= 2000
- -10<sup>6</sup> <= nums[i] <= 10<sup>6</sup>

******************************
**Explanation**
- 2-D dp: in the second dimension, use 2 variables to record the state
- 0 is for keeping tracking of the current length of longest increasing subsequence, 1 is for keeping track of the count of the length
- dp[i][0] = max(dp[j][0] + 1, dp[i][0])
- dp[i][1] depends on the comparison of dp[i][0] and dp[j][0]+1

**Python**

```python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [[1, 1] for _ in range(n)]
        longestSub = 1
        for i in range(n):
            for j in range(i):
                if nums[i] > nums[j]:
                    if dp[i][0] < dp[j][0] + 1:
                        dp[i][0] = dp[j][0] + 1
                        dp[i][1] = dp[j][1] # 
                    elif  dp[i][0] == dp[j][0] + 1:
                        dp[i][1] += dp[j][1] # 
            longestSub = max(longestSub, dp[i][0])
             
        count = 0
        for i in range(n):
            if dp[i][0] == longestSub:
                count += dp[i][1]
        return count
```

**Complexity**:

- Time Complexity: ```O(n^2)```
- Space Complexity: ```O(n)```
