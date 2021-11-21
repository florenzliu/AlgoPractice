### [Triple Inversion](https://binarysearch.com/problems/Triple-Inversion)
Given a list of integers nums, return the number of pairs i < j such that nums[i] > nums[j] * 3.

**Example 1:**

```
Input: nums = [7, 1, 2]
Output: 2
Explanation:
We have the pairs (7, 1) and (7, 2)
```

**Constraints:**

- n ≤ 100,000 where n is the length of nums

******************************
**Explanation**
- approach 1: brute force, time O(N<sup>2</sup>), space O(1)
- approach 2: sorted list and binary search, time O(N<sup>2</sup>) due to insertion, space O(N)
- approach 3: mergeSort, time O(NlogN), space O(N)

**Python**

```python
class Solution:
    def solve(self, nums):
        def mergeSort(start, end, temp):
            if start < end:
                mid = start + (end-start)//2
                mergeSort(start, mid, temp)
                mergeSort(mid+1, end, temp)
                merge(start, mid, end, temp)
        
        def merge(start, mid, end, temp):
            nonlocal count
            i, j = start, mid+1
            while i <= mid and j <= end:
                if nums[i] <= nums[j]:
                    temp.append(nums[i])
                    i += 1
                else:
                    temp.append(nums[j])
                    j += 1
            
            ti, tj = start, mid+1
            while ti <= mid and tj <= end:
                if nums[ti] <= nums[tj] * 3:
                    ti += 1
                else:
                    count += mid - ti + 1
                    tj += 1

            while i <= mid:
                temp.append(nums[i])
                i += 1
            while j <= end:
                temp.append(nums[j])
                j += 1
            for i in range(len(temp)):
                nums[start+i] = temp[i]
            temp.clear()
        
        count = 0
        mergeSort(0, len(nums)-1, [])
        return count
```

**Complexity**:

- Time Complexity: ```O(NlogN)```
- Space Complexity: ```O(N)```
