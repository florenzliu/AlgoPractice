### Leetcode 62. [Unique Paths](https://leetcode.com/problems/unique-paths/)
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)
```
Input: m = 3, n = 7
Output: 28
```

**Example 2:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```

**Example 3:**
```
Input: m = 7, n = 3
Output: 28
```

**Example 4:**
```
Input: m = 3, n = 3
Output: 6
```

**Constraints:**

- 1 <= m, n <= 100
- It's guaranteed that the answer will be less than or equal to 2 * 10<sup>9</sup>.

******************************
**Explanation**
- dp[i][j]: the total number of unique paths to reach cell[i][j]
- to reach cell[i][j], its last step is either from the left or from the top: dp[i][j] = dp[i-1][j] + dp[i][j-1]

**Python**

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for _ in range(n)] for _ in range(m)]
        
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i][j-1] + dp[i-1][j]
        return dp[-1][-1]
```

**Complexity**:

- Time Complexity: ```O(mn)```
- Space Complexity: ```O(mn)```
