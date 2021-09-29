### Leetcode 447. [Number of Boomerangs](https://leetcode.com/problems/number-of-boomerangs/)
You are given n points in the plane that are all distinct, where points[i] = [xi, yi]. A boomerang is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Return the number of boomerangs.


**Example 1:**

Input: points = [[0,0],[1,0],[2,0]]\
Output: 2\
Explanation: The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]].

**Example 2:**

Input: points = [[1,1],[2,2],[3,3]]\
Output: 2

**Example 3:**

Input: points = [[1,1]]
Output: 0

**Constraints:**

- n == points.length
- 1 <= n <= 500
- points[i].length == 2
- -10<sup>4</sup> <= x<sub>i</sub>, y<sub>i</sub> <= 10<sup>4</sup>
- All the points are unique.

******************************
**Explanation**
- Calculate the distance between every two points
- Use a hashmap to store the count of points that have the same distance from the current point
- Since the order matters, use permutation for each count

**Python**

```python
class Solution:
    def numberOfBoomerangs(self, points: List[List[int]]) -> int:
        n = len(points)
        count = 0
        for i in range(n):
            d = defaultdict(int)
            for j in range(n):
                distance = (points[i][0] - points[j][0]) ** 2 + (points[i][1] - points[j][1]) ** 2
                d[distance] += 1
            for k in d.keys():
                count += d[k] * (d[k] - 1)
        return count
```

**Complexity**:

- Time Complexity: O(N<sup>2</sup>)
- Space Complexity: O(N)
