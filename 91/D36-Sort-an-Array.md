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
        # merge sort: O(nlogn), space O(n)
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
        
        # quick sort: O(nlogn), space O(1)
        # quick sort: pick the last element as pivot, use partition function, quicksort before, quicksort after,  T(n) = T(k) + T(n-k-1) + \theta(n)
        def quickSort(start, end, arr): # start and end included
            if start < end:
                pivot = partition(start, end, arr)
                quickSort(start, pivot-1, arr)
                quickSort(pivot+1, end, arr)
            
        def partition(start, end, arr): # use the last element as pivot
            pivot = arr[end]
            pointer = start - 1
            for i in range(start, end+1):
                if arr[i] < pivot:
                    pointer += 1
                    arr[pointer], arr[i] = arr[i], arr[pointer]
            arr[pointer+1], arr[end] = arr[end], arr[pointer+1]
            return pointer+1
             
        quickSort(0, len(nums)-1, nums)
        return nums
        
        # heap sort: O(nlogn), space O(1)
        def heapSort(arr):
            # build a maxheap
            for i in range(len(arr)//2-1, -1, -1):
                heapify(arr, len(arr), i)
            
            for i in range(len(arr)-1, -1, -1):
                arr[i], arr[0] = arr[0], arr[i]
                heapify(arr, i, 0)
        
        def heapify(arr, n, i):
            largest = i
            left = i * 2 + 1
            right = i * 2 + 2
            
            if left < n and arr[largest] < arr[left]:
                largest = left
            if right < n and arr[largest] < arr[right]:
                largest = right
            
            if largest != i:
                arr[i], arr[largest] = arr[largest], arr[i]
                heapify(arr, n, largest)
        
        heapSort(nums)
        return nums
        
        
        # selection sort: O(n^2), space O(1)
        # pick a minimum element from the remaining unsorted array to add to the sorted array at each iteration
        for i in range(len(nums)):
            currMin = math.inf
            for j in range(i, len(nums)):
                if nums[j] < currMin:
                    currMin = nums[j]
                    pos = j
            nums[i], nums[pos] = nums[pos], nums[i]
        return nums

        # insertion sort: : O(n^2), space O(1)
        # compare an element with all its previous elements and move those with higher values to their next position at each iteration
        for i in range(1, len(nums)):
            if nums[i] < nums[i-1]:
                for j in range(i, 0, -1):
                    if nums[j] < nums[j-1]:
                        nums[j], nums[j-1] = nums[j-1], nums[j]
                    else:
                        break
        return nums
```

**Complexity**:

- Time Complexity: ```O(NlogN)```
- Space Complexity: ```O(N)```
