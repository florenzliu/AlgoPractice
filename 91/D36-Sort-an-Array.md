### Leetcode 912. [Sort an Array](https://leetcode.com/problems/sort-an-array/)
Given an array of integers nums, sort the array in ascending order.

**Example 1:**

```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
```

**Example 2:**

```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

**Constraints:**

- 1 <= nums.length <= 5 * 10<sup>4</sup>
- -5 * 10<sup>4</sup> <= nums[i] <= 5 * 10<sup>4</sup>

******************************
**Explanation**
- use mergeSort
- divide and conquer: merge sort left, merge sort right, then merge the sorted left and right into one sorted array
- T(n) = 2T(n/2) + θ(n)

**Python**

```python
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        def mergeSort(start, end, arr): 
            if start < end:
                mid = start + (end - start) // 2
                mergeSort(start, mid, arr)
                mergeSort(mid+1, end, arr)
                merge(start, mid, end, arr)
                
        def merge(start, mid, end, arr):
            temp = [0 for _ in range(end - start + 1)]
            leftIndex, rightIndex = start, mid+1
            curr = 0
            while leftIndex < mid+1 and rightIndex < end+1:
                if arr[leftIndex] <= arr[rightIndex]:
                    temp[curr] = arr[leftIndex]
                    leftIndex += 1
                else:
                    temp[curr] = arr[rightIndex]
                    rightIndex += 1
                curr += 1
            
            while leftIndex < mid+1:
                temp[curr] = arr[leftIndex]
                leftIndex += 1
                curr += 1

            while rightIndex < end+1:
                temp[curr] = arr[rightIndex]
                rightIndex += 1
                curr += 1
           
            # copy temp to arr
            for i in range(start, end+1):
                arr[i] = temp[i-start]
                
        mergeSort(0, len(nums)-1, nums)
        return nums
```

**Complexity**:

- Time Complexity: ```O(NlogN)```
- Space Complexity: ```O(N)```
