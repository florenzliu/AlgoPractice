### Leetcode 322. [Coin Change](https://leetcode.com/problems/coin-change/)
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1
```

**Example 3:**

```
Input: coins = [1], amount = 0
Output: 0
```

**Example 4:**

```
Input: coins = [1], amount = 1
Output: 1
```

**Example 5:**

```
Input: coins = [1], amount = 2
Output: 2
```

**Constraints:**

- 1 <= coins.length <= 12
- 1 <= coins[i] <= 2<sup>31</sup> - 1
- 0 <= amount <= 10<sup>4</sup>

******************************
**Explanation**
- knapsack problem using 1-D dp
  - dp[i]: the fewest number of coins that you need to make up the amount i
- trick: start with coins in the first loop

**Python**

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [math.inf for i in range(amount+1)]
        dp[0] = 0
        
        for c in coins:
            for i in range(c, amount+1):
                dp[i] = min(dp[i], dp[i-c]+1)
        
        return dp[-1] if dp[-1] != math.inf else -1
```

**Complexity**:

- Time Complexity: ```O(mn)``` where m is the amount and n is the length of the coins list
- Space Complexity: ```O(m)```
