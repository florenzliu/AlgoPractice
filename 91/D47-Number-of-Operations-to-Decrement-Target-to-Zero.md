### [Number of Operations to Decrement Target to Zero](https://binarysearch.com/problems/Number-of-Operations-to-Decrement-Target-to-Zero)
You are given a list of positive integers nums and an integer target. Consider an operation where we remove a number v from either the front or the back of nums and decrement target by v.

Return the minimum number of operations required to decrement target to zero. If it's not possible, return -1.

**Example 1:**

```
Input: 
nums = [3, 1, 1, 2, 5, 1, 1]
target = 7
Output: 3
Explanation:
We can remove 1, 1 and 5 from the back to decrement target to zero.
```

**Example 1:**

```
Input: 
nums = [2, 4]
target = 7
Output: -1
Explanation:
There's no way to decrement target = 7 to zero.
```

**Constraints:**

- n ≤ 100,000 where n is the length of nums

******************************
**Explanation**
- the minimum number of operations to reach target =  the maximum length of sublist that equals to sum(nums) - target
- use sliding window to get the current sum
  - if equal, update the maximum length
  - if larger than sum(nums)-target, reduce window size by moving left pointer forward
- finally return len(nums) - maxLength

**Python**

```python
class Solution:
    def solve(self, nums, target):
        s = sum(nums)
        if s == target: 
            return len(nums)
        elif s < target:
            return -1
        else:
            maxLength = 0
            newTarget = sum(nums) - target
            left, currSum = 0, 0
            for i in range(len(nums)):
                currSum += nums[i]
                while currSum > newTarget:
                    currSum -= nums[left]
                    left += 1
                if currSum == newTarget:
                    maxLength = max(maxLength, i-left+1)
            return len(nums)-maxLength if maxLength != 0 else -1
```

**Complexity**:

- Time Complexity: ```O(N)```
- Space Complexity: ```O(1)```
