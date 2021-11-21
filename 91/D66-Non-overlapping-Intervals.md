### Leetcode 435. [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)
Given an array of intervals intervals where intervals[i] = [starti, endi], return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

**Example 1:**

```
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.
```

**Example 2:**

```
Input: intervals = [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to make the rest of the intervals non-overlapping.
```

**Example 2:**

```
Input: intervals = [[1,2],[2,3]]
Output: 0
Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
```

**Constraints:**

- 1 <= intervals.length <= 10<sup>5</sup>
- intervals[i].length == 2
- -5 * 10<sup>4</sup> <= start<sub>i</sub> < end<sub>i</sub> <= 5 * 10<sup>4</sup>

******************************
**Explanation**
- dfs: 2^n
- dp: n^2
- greedy + LIS: nlogn

**Python**

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        if len(intervals) == 0:
            return 0
        
        intervals.sort()
        ans = 1
        
        def lenOfLIS(l):
            d = []
            for start, end in l:
                i = bisect.bisect_left(d, end)
                if i < len(d):
                    d[i] = end
                elif not d or d[-1] <= start:
                    d.append(end)
            return len(d)
        
        return len(intervals) - lenOfLIS(intervals)
```

**Complexity**:

- Time Complexity: ```O(nlogn)```
- Space Complexity: ```O(n)```
