### Leetcode 347. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

**Example 1:**

Input: nums = [1,1,1,2,2,3], k = 2\
Output: [1,2]

**Example 2:**

Input: nums = [1], k = 1\
Output: [1]

**Constraints:**

- 1 <= nums.length <= 10<sup>5</sup>
- k is in the range [1, the number of unique elements in the array].
- It is guaranteed that the answer is unique.

******************************
**Explanation**
- Approach 1: use a hashmap to store all the numbers and count its frequency, then sort by its frequency and return the first k keys
- Approach 2: use a heap, return the first k elements

**Python**

```python
# Approach 1
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        result = []
        d = defaultdict(int)
        for n in nums:
            d[n] += 1
        for i in sorted(d.items(), key=lambda item: item[1], reverse=True):
            if k == 0:
                return result
            result.append(i[0])
            k -= 1
        return result

# Approach 2

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        if k == len(nums):
            return nums
        count = Counter(nums)
        return heapq.nlargest(k, count.keys(), key=count.get)

```

**Complexity**

Approach 1:
- Time Complexity: ```O(N)```
- Space Complexity: ```O(N)``` 

Approach 2:
- Time complexity: ```O(Nlogk)``` if k < N and ```O(N)``` if k = N
- Space complexity: ```O(N + k)```