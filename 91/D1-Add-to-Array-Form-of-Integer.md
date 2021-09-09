## Leetcode 989. Add to Array-Form of Integer

The array-form of an integer num is an array representing its digits in left to right order.

For example, for num = 1321, the array form is [1,3,2,1].\
Given num, the array-form of an integer, and an integer k, return the array-form of the integer num + k.

**Example 1:**

Input: num = [1,2,0,0], k = 34\
Output: [1,2,3,4]\
Explanation: 1200 + 34 = 1234

**Example 2:**

Input: num = [2,7,4], k = 181\
Output: [4,5,5]\
Explanation: 274 + 181 = 455

**Example 3:**

Input: num = [2,1,5], k = 806\
Output: [1,0,2,1]\
Explanation: 215 + 806 = 1021

**Example 4:**

Input: num = [9,9,9,9,9,9,9,9,9,9], k = 1\
Output: [1,0,0,0,0,0,0,0,0,0,0]\
Explanation: 9999999999 + 1 = 10000000000
 

**Constraints:**

1 <= num.length <= 104\
0 <= num[i] <= 9\
num does not contain any leading zeros except for the zero itself.\
1 <= k <= 104

******************************
**Explanation**

- Convert k to its array-form. 
- Add the array-forms of num and k by digit from the end to the beginning and save it in the result array. 
- Reverse the array-form of the result. 

Use the quotient and remainder divided by 10: set the current position as the remainder and update the quotient for the next position.

**Python**

```
class Solution:
    def addToArrayForm(self, num: List[int], k: int) -> List[int]:
        newK = []
        for i in str(k):
            newK.append(int(i))
        
        result = []
        i, j = len(num)-1, len(newK)-1
        quotient, remainder = 0, 0
        while i >= 0 or j >= 0:
            currI = num[i] if i >= 0 else 0
            currJ = newK[j] if j >= 0 else 0
            curr = currI + currJ + quotient
            result.append(curr % 10)
            quotient = curr // 10
            i -= 1
            j -= 1
            
        if quotient != 0:
            result.append(quotient)
        return result[::-1]
```

**Complexity**

- Time Complexity: ```O(max(N, logk))``` where ```N``` is the length of the ```num``` array and ```logk``` is the length of the array-form of ```k```.
- Space Complexity: ```O(max(N, logk))``` 
