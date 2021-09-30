### Leetcode 768. [Max Chunks To Make Sorted II](https://leetcode.com/problems/max-chunks-to-make-sorted-ii/)

You are given an integer array arr.

We split arr into some number of chunks (i.e., partitions), and individually sort each chunk. After concatenating them, the result should equal the sorted array.

Return the largest number of chunks we can make to sort the array.

 

**Example 1:**

Input: arr = [5,4,3,2,1]\
Output: 1\
Explanation:\
Splitting into two or more chunks will not return the required result.
For example, splitting into [5, 4], [3, 2, 1] will result in [4, 5, 1, 2, 3], which isn't sorted.

**Example 2:**

Input: arr = [2,1,3,4,4]\
Output: 4\
Explanation:
We can split into two chunks, such as [2, 1], [3, 4, 4].
However, splitting into [2, 1], [3], [4], [4] is the highest number of chunks possible.
 

**Constraints:**

1 <= arr.length <= 2000\
0 <= arr[i] <= 10<sup>8</sup>
 
******************************
**Explanation**
- Use a monotonically increasing stack to save the largest value in each partitioned chunk.
- When encountering a smaller element, pop out the elements in the stack until the last one is smaller than the current element. Otherwise, add it to the stack.
- Return the length of the stack as the final answer.

**Python**

```python
class Solution:
    def maxChunksToSorted(self, arr: List[int]) -> int:        
        stack = []
        for i in range(len(arr)):
            if stack and stack[-1] > arr[i]:
                curr = stack[-1]
                while stack and stack[-1] > arr[i]:
                    stack.pop()
                stack.append(curr)
            else:
                stack.append(arr[i])
                
        return len(stack)
```

**Complexity**

- Time Complexity: ```O(N)``` 
- Space Complexity: ```O(N)``` 
