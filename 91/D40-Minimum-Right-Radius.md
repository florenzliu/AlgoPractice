### [Minimum Right Radius](https://binarysearch.com/problems/Minimum-Light-Radius)
You are given a list of integers nums representing coordinates of houses on a 1-dimensional line. You have 3 street lights that you can put anywhere on the coordinate line and a light at coordinate x lights up houses in [x - r, x + r], inclusive. Return the smallest r required such that we can place the 3 lights and all the houses are lit up.

**Example 1:**

```
Input: nums = [3, 4, 5, 6]
Output: 0.5
Explanation:
If we place the lamps on 3.5, 4.5 and 5.5 then with r = 0.5 we can light up all 4 houses.
```

**Constraints:**

- n ≤ 100,000 where n is the length of nums

******************************
**Explanation**
- find the range of r: [0, max(nums)-min(nums)]
- use binary search to find the minimum possible r
  - sort the list ```nums``` and binary search the insertion index of the current r
  - update the position of the next light and search for its insertion index
  - compare with the length of the list ```nums```, if longer than its length, possible, otherwise, return False

**Python**

```python
class Solution:
    def solve(self, nums):
        if len(nums) < 2:
            return 0
        
        nums.sort()
        
        def possible(d):
            start = nums[0]
            end = start + d
            for i in range(3):
                index = bisect.bisect_right(nums, end)
                if index >= len(nums):
                    return True
                start = nums[index]
                end = start + d
            return False

        l, r = 0, nums[-1] - nums[0]
        while l <= r:
            mid = l + (r-l)//2
            if possible(mid):
                r = mid - 1
            else:
                l = mid + 1
        return l / 2
```

**Complexity**:

- Time Complexity: ```O(NlogN)```
- Space Complexity: ```O(1)```
