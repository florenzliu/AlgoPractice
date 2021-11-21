### Leetcode 695. [Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
You are given an m x n binary matrix grid. An island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The area of an island is the number of cells with a value 1 in the island.

Return the maximum area of an island in grid. If there is no island, return 0.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)
```
Input: grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output: 6
Explanation: The answer is not 11, because the island must be connected 4-directionally.
```

**Example 2:**

```
Input: grid = [[0,0,0,0,0,0,0,0]]
Output: 0
```

**Constraints:**

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 50
- grid[i][j] is either 0 or 1.

******************************
**Explanation**
- dfs
- change island (1) to -1 after visiting

**Python**

```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        row, col = len(grid), len(grid[0])
        
        def dfs(m, n, grid):
            nonlocal count
            if m < row and n < col and m >= 0 and n >= 0 and grid[m][n] == 1:
                count += 1
                grid[m][n] = -1
                dfs(m-1, n, grid)
                dfs(m+1, n, grid)
                dfs(m, n-1, grid)
                dfs(m, n+1, grid)
            return
            
        maxArea = 0
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 1:
                    count = 0
                    dfs(i, j, grid)
                    maxArea = max(count, maxArea)
        return maxArea
```

**Complexity**:

- Time Complexity: ```O(mn)``` where m and n are the row and column of the grid, respectively
- Space Complexity: ```O(mn)```
