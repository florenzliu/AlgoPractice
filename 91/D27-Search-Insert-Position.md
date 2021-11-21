
### Leetcode 35. [Search Insert Position](https://leetcode.com/problems/search-insert-position/)
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

**Example 1:**

```
IInput: nums = [1,3,5,6], target = 5
Output: 2
```

**Example 2:**

```
Input: nums = [1,3,5,6], target = 2
Output: 1
```

**Example 3:**

```
Input: nums = [1,3,5,6], target = 7
Output: 4
```

**Example 4:**

```
Input: nums = [1,3,5,6], target = 0
Output: 0
```

**Example 5:**

```
Input: nums = [1], target = 0
Output: 0
```

**Constraints:**

- 1 <= nums.length <= 10<sup>4</sup>
- -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
- nums contains distinct values sorted in ascending order.
- -10<sup>4</sup> <= target <= 10<sup>4</sup>

******************************
**Explanation**
- since the list is sorted, use binary search
- at each round, find the mid point
  - if the mid point is equal to target, return the index of the mid point
  - if the mid point is larger than target, search the remaining left side of the mid point
  - if the mid point is smaller than target, search the remaining right side of the mid point
- stop when the start point is larger than the end point, and return start point as the insertion position

**Python**

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        def bsearch(start, end, target):
            if start > end:
                return start
            mid = (start + end) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                return bsearch(start, mid-1, target)
            else:
                return bsearch(mid+1, end, target)
        return bsearch(0, len(nums)-1, target)
```

**Complexity**:

- Time Complexity: ```O(logN)```
- Space Complexity: ```O(1)```
