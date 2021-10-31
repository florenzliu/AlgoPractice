### Leetcode 1162. [As Far from Land as Possible](https://leetcode.com/problems/as-far-from-land-as-possible/)
Given an n x n grid containing only values 0 and 1, where 0 represents water and 1 represents land, find a water cell such that its distance to the nearest land cell is maximized, and return the distance. If no land or water exists in the grid, return -1.

The distance used in this problem is the Manhattan distance: the distance between two cells (x0, y0) and (x1, y1) is |x0 - x1| + |y0 - y1|.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/05/03/1336_ex1.JPG)
```
Input: grid = [[1,0,1],[0,0,0],[1,0,1]]
Output: 2
Explanation: The cell (1, 1) is as far as possible from all the land with distance 2.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/05/03/1336_ex2.JPG)

```
Input: grid = [[1,0,0],[0,0,0],[0,0,0]]
Output: 4
Explanation: The cell (2, 2) is as far as possible from all the land with distance 4.
```

**Constraints:**

- n == grid.length
- n == grid[i].length
- 1 <= n <= 100
- grid[i][j] is 0 or 1

******************************
**Explanation**
- bfs
- start with all the lands at the same time
- change island (1) to -1 after visiting

**Python**

```python
class Solution:
    def maxDistance(self, grid: List[List[int]]) -> int:
        row, col = len(grid), len(grid[0])
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        
        def isValid(r, c):
            return r < row and c < col and r >= 0 and c >= 0
        
        queue = []
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 1:
                    queue.append((i, j))
        
        if len(queue) == row * col or len(queue) == 0:
            return -1
        
        dist = -1
        while queue:
            n = len(queue)
            for _ in range(n):
                x, y = queue.pop(0)
                for d in directions:
                    newX, newY = x+d[0], y+d[1]
                    if isValid(newX, newY) and grid[newX][newY] == 0:
                        grid[newX][newY] = -1
                        queue.append((newX, newY))
            dist += 1
        return dist
```

**Complexity**:

- Time Complexity: ```O(n^2)```
- Space Complexity: ```O(n^2)```
