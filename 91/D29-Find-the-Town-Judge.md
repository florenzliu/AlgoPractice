### Leetcode 997. [Find the Town Judge](https://leetcode.com/problems/find-the-town-judge/)
In a town, there are n people labeled from 1 to n. There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

1. The town judge trusts nobody.
2. Everybody (except for the town judge) trusts the town judge.
3. There is exactly one person that satisfies properties 1 and 2.

You are given an array trust where trust[i] = [ai, bi] representing that the person labeled ai trusts the person labeled bi.

Return the label of the town judge if the town judge exists and can be identified, or return -1 otherwise.

**Example 1:**

```
Input: n = 2, trust = [[1,2]]
Output: 2
```

**Example 2:**

```
Input: n = 3, trust = [[1,3],[2,3]]
Output: 3
```

**Example 3:**

```
Input: n = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
```

**Example 4:**

```
Input: n = 3, trust = [[1,2],[2,3]]
Output: -1
```

**Example 5:**

```
Input: n = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
Output: 3
```

**Constraints:**

- 1 <= n <= 1000
- 0 <= trust.length <= 10<sup>4</sup>
- trust[i].length == 2
- All the pairs of trust are unique.
- ai != bi
- 1 <= ai, bi <= n

******************************
**Explanation**
- although it looks like a graph problem, we can simplify it by just looking at the outdegree and indegree of each node
- use an array to keep track of the indegree for each node
- update a node to -1 if it has outdegree
- traverse the array and return the one with indegree = n-1

**Python**

```python
class Solution:
    def findJudge(self, n: int, trust: List[List[int]]) -> int:
        arr = [0 for _ in range(n)]
        for a, b in trust:
            if arr[b-1] != -1:
                arr[b-1] += 1
            arr[a-1] = -1
    
        for i in range(n):
            if arr[i] == n-1:
                return i+1 
        return -1
```

**Complexity**:

- Time Complexity: ```O(N)```
- Space Complexity: ```O(N)```
