### Leetcode 198. [House Robber](https://leetcode.com/problems/house-robber/)
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
```

**Constraints:**

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 400

******************************
**Explanation**
- 1-D dp
- dp[i] = max(dp[i-1], dp[i-2] + nums[i])
- space complexity can be reduced to 1

**Python**

```python
class Solution:
    # Approach 1 (space O(n))
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
        elif len(nums) == 2:
            return max(nums)
        else:
            dp = [0 for _ in range(len(nums))]
            dp[0], dp[1] = nums[0], max(nums[0], nums[1])
            for i in range(2, len(nums)):
                dp[i] = max(dp[i-1], dp[i-2]+nums[i])  
            return max(dp[-1], dp[-2])
    # Approach 2 (space O(1))
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
        elif len(nums) == 2:
            return max(nums)
        else:
            prevprev, prev = nums[0], max(nums[0], nums[1])
            for i in range(2, len(nums)):
                temp = max(prev, prevprev+nums[i]) 
                prevprev = prev
                prev = temp
            return max(prev, prevprev)
```

**Complexity**:

- Time Complexity: ```O(n)```
- Space Complexity: ```O(n) / O(1)```
