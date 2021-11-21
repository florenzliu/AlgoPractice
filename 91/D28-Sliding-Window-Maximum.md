### Leetcode 239. [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

**Example 1:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

**Example 3:**

```
Input: nums = [1,-1], k = 1
Output: [1,-1]
```

**Example 4:**

```
Input: nums = [9,11], k = 2
Output: [11]
```

**Example 5:**

```
Input: nums = [4,-2], k = 2
Output: [4]
```

**Constraints:**

- -1 <= nums.length <= 10<sup>5</sup>
- -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
- 1 <= k <= nums.length

******************************
**Explanation**
- use a deque as a monotonically decreasing stack to keep track of the indices of numbers that are in the sliding window
- at each index
  - pop out all the numbers in the sliding window that is smaller than the current number from the end
  - pop out the largest numbers that are outside the sliding window from the front
  - append the current numbers to the deque
  - if current index is larger than k-1, append the largest number in the deque (the first one) in the result list

**Python**

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        deque = collections.deque()
        result = []
        for i in range(len(nums)):  
            while deque and nums[deque[-1]] < nums[i]:
                deque.pop()
            while deque and deque[0] <= i - k:
                deque.popleft()   
            deque.append(i)
            if i >= k-1:
                result.append(nums[deque[0]])
        return result
```

**Complexity**:

- Time Complexity: ```O(N)```
- Space Complexity: ```O(N)```
