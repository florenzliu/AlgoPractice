### Leetcode 886. [Possible Bipartition](https://leetcode.com/problems/possible-bipartition/)
We want to split a group of n people (labeled from 1 to n) into two groups of any size. Each person may dislike some other people, and they should not go into the same group.

Given the integer n and the array dislikes where dislikes[i] = [ai, bi] indicates that the person labeled ai does not like the person labeled bi, return true if it is possible to split everyone into two groups in this way.

**Example 1:**

```
Input: n = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4] and group2 [2,3].
```

**Example 2:**

```
Input: n = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false
```

**Example 3:**

```
Input: n = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false
```

**Constraints:**

- 1 <= n <= 2000
- 0 <= dislikes.length <= 10<sup>4</sup>
- dislikes[i].length == 2
- 1 <= dislikes[i][j] <= n
- ai < bi
- All the pairs of dislikes are unique.

******************************
**Explanation**
- first, build adjacency list of the graph
- use coloring algorithm to slit people into 2 groups:
  - 1 for the first group
  - -1 for the second group
  - 0 for not-visited-yet vertices
- use bfs to traverse each level and check if the neighbouring vertices have the same color

**Python**

```python
class Solution:
    def possibleBipartition(self, n: int, dislikes: List[List[int]]) -> bool:
        d = defaultdict(list)
        for a, b in dislikes:
            d[a].append(b)
            d[b].append(a)
        
        color = [0 for i in range(n+1)]
        for i in range(1, n+1):
            if color[i] == 0:
                color[i] = 1
                queue = [i]
                while queue:
                    curr = queue.pop(0)
                    for num in d[curr]:
                        if color[num] == color[curr]:
                            return False
                        if color[num] == 0:
                            color[num] = -color[curr]
                            queue.append(num)
        return True
```

**Complexity**:

- Time Complexity: ```O(V+E)```
- Space Complexity: ```O(V+E)```
