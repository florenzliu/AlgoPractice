### [Shorted Cycle Containing Target Node](https://binarysearch.com/problems/Shortest-Cycle-Containing-Target-Node)
You are given a two-dimensional list of integers graph representing a directed graph as an adjacency list. You are also given an integer target.

Return the length of a shortest cycle that contains target. If a solution does not exist, return -1.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)
```
Input: graph = [
    [1],
    [2],
    [0]
]
target = 0
Output: 3
Explanation:
The nodes 0 -> 1 -> 2 -> 0 form a cycle
```

**Example 2:**

```
Input: graph = [
    [1],
    [2],
    [4],
    [],
    [0]
]
target = 3
Output: -1
```

**Constraints:**

- n, m ≤ 250 where n and m are the number of rows and columns in graph

******************************
**Explanation**
- bfs

**Python**

```python
class Solution:
    def solve(self, graph, target):
        queue = [target]
        dist = 0
        visited = [0 for _ in range(len(graph))]
        while queue:
            for _ in range(len(queue)):
                curr = queue.pop(0)
                visited[curr] = 1
                for neighbour in graph[curr]:
                    if neighbour == target:
                        return dist + 1
                    if not visited[neighbour]:
                        queue.append(neighbour)  
            dist += 1
        return -1
```

**Complexity**:

- Time Complexity: ```O(V+E)```
- Space Complexity: ```O(V+E)```
