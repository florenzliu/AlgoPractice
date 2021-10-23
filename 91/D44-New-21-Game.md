### Leetcode 837. [New 21 Game](https://leetcode.com/problems/new-21-game/)
Alice plays the following game, loosely based on the card game "21".

Alice starts with 0 points and draws numbers while she has less than k points. During each draw, she gains an integer number of points randomly from the range [1, maxPts], where maxPts is an integer. Each draw is independent and the outcomes have equal probabilities.

Alice stops drawing numbers when she gets k or more points.

Return the probability that Alice has n or fewer points.

Answers within 10-5 of the actual answer are considered accepted.

**Example 1:**

```
Input: n = 10, k = 1, maxPts = 10
Output: 1.00000
Explanation: Alice gets a single card, then stops.
```

**Example 2:**

```
Input: n = 6, k = 1, maxPts = 10
Output: 0.60000
Explanation: Alice gets a single card, then stops.
In 6 out of 10 possibilities, she is at or below 6 points.
```

**Example 3:**

```
Input: n = 21, k = 17, maxPts = 10
Output: 0.73278
```

**Constraints:**

- 0 <= k <= n <= 10<sup>4</sup>
- 1 <= maxPts <= 10<sup>4</sup>

******************************
**Explanation**
- dp + sliding window
- dp[i]: the probability that Alice's score (i.e., i) is not greater than N
- dp[i] = (dp[i+1] + dp[i+2] + ... + dp[i+W]) / W
- The objective is to get the score x where K <= x <= N

**Python**

```python
class Solution:
    def new21Game(self, N: int, K: int, W: int) -> float:
        dp = [0 for _ in range(K + W)]
        
        curr_sum = 0
        for i in range(K, K+W):
            if i <= N:
                dp[i] = 1
            curr_sum += dp[i]
        
        for i in range(K-1, -1, -1):
            dp[i] = curr_sum / W
            curr_sum += dp[i] - dp[i+W]
            
        return dp[0]
```

**Complexity**:

- Time Complexity: ```O(K+W)```
- Space Complexity: ```O(K+W)```
