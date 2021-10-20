### [Kth Pair Distance](https://binarysearch.com/problems/Kth-Pair-Distance)
Given a list of integers nums and an integer k, return the k-th (0-indexed) smallest abs(x - y) for every pair of elements (x, y) in nums. Note that (x, y) and (y, x) are considered the same pair.

**Example 1:**

```
Input: nums = [1, 5, 3, 2]
k = 3
Output: 2
Explanation:
Here are all the pair distances:

abs(1 - 5) = 4
abs(1 - 3) = 2
abs(1 - 2) = 1
abs(5 - 3) = 2
abs(5 - 2) = 3
abs(3 - 2) = 1
Sorted in ascending order we have [1, 1, 2, 2, 3, 4].
```

**Constraints:**

- n ≤ 100,000 where n is the length of nums

******************************
**Explanation**
- binary search + two pointers
- range: 0 ~ max(nums) - min(nums)
- for each possible difference in the above range, find out if there are exactly k values less than the difference

**Python**

```python
class Solution:
    def solve(self, nums, k):
        nums.sort()
        def helper(target):
            count = 0
            prev = 0
            for i in range(1, len(nums)):
                while nums[i] - nums[prev] > target:
                    prev += 1
                count += i - prev
            return count

        start, end = 0, nums[-1] - nums[0]
        while start <= end:
            mid = start + (end - start) // 2
            if helper(mid) > k:
                end = mid - 1
            else:
                start = mid + 1
        return start
```

**Complexity**:

- Time Complexity: ```O(NlogN)```
- Space Complexity: ```O(1)```
