### Leetcode 1203. [Sort Items by Groups Respecting Dependencies](https://leetcode.com/problems/sort-items-by-groups-respecting-dependencies/)
There are n items each belonging to zero or one of m groups where group[i] is the group that the i-th item belongs to and it's equal to -1 if the i-th item belongs to no group. The items and the groups are zero indexed. A group can have no item belonging to it.

Return a sorted list of the items such that:

- The items that belong to the same group are next to each other in the sorted list.
- There are some relations between these items where beforeItems[i] is a list containing all the items that should come before the i-th item in the sorted array (to the left of the i-th item).

Return any solution if there is more than one solution and return an empty list if there is no solution.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/09/11/1359_ex1.png)
```
Input: n = 8, m = 2, group = [-1,-1,1,0,0,1,0,-1], beforeItems = [[],[6],[5],[6],[3,6],[],[],[]]
Output: [6,3,4,1,5,2,0,7]
```

**Example 2:**

```
Input: n = 8, m = 2, group = [-1,-1,1,0,0,1,0,-1], beforeItems = [[],[6],[5],[6],[3],[],[4],[]]
Output: []
Explanation: This is the same as example 1 except that 4 needs to be before 6 in the sorted list.
```

**Constraints:**

- 1 <= m <= n <= 3 * 10<sup>4</sup>
- group.length == beforeItems.length == n
- -1 <= group[i] <= m - 1
- 0 <= beforeItems[i].length <= n - 1
- 0 <= beforeItems[i][j] <= n - 1
- i != beforeItems[i][j]
- beforeItems[i] does not contain duplicates elements.

******************************
**Explanation**
- first, assign the teams with no group a new group number
- second, build directed graphs for items and groups and then topological sort items and groups
- third, find order of items within each group and combine the ordered items from each group

**Python**

```python
class class Solution:
    def sortItems(self, n: int, m: int, group: List[int], beforeItems: List[List[int]]) -> List[int]:
       def topSort(deg, graph):
            stack = [v for v in range(len(graph)) if deg[v] == 0]
            res = []
            while stack:
                curr = stack.pop()
                res.append(curr)
                for v in graph[curr]:
                    deg[v] -= 1
                    if deg[v] == 0:
                        stack.append(v)
            return res if len(res) == len(graph) else []
        
        for i in range(len(group)):
            if group[i] == -1:
                group[i] = m
                m += 1
        
        groupGraph = [[] for _ in range(m)]
        itemGraph = [[] for _ in range(n)]
        groupDegree = [0] * m
        itemDegree = [0] * n
        
        for i in range(n):
            for item in beforeItems[i]:
                itemGraph[item].append(i)
                itemDegree[i] += 1
                if group[item] != group[i]:
                    groupDegree[group[i]] += 1
                    groupGraph[group[item]].append(group[i])
                    
        groupTopSort = topSort(groupDegree, groupGraph)
        itemTopSort = topSort(itemDegree, itemGraph)
        
        if not groupTopSort or not itemTopSort:
            return []
        
        orderInGroup = defaultdict(list)
        for i in itemTopSort:
            orderInGroup[group[i]].append(i)
        
        ans = []
        for j in groupTopSort:
            ans += orderInGroup[j]
            
        return ans
```

**Complexity**:

- Time Complexity: ```O(m+n)```
- Space Complexity: ```O(m+n)```
