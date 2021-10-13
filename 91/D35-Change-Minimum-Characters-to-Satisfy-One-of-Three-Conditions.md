### Leetcode 1737. [Change Minimum Characters to Satisfy One of Three Conditions](https://leetcode.com/problems/change-minimum-characters-to-satisfy-one-of-three-conditions/)
You are given two strings a and b that consist of lowercase letters. In one operation, you can change any character in a or b to any lowercase letter.

Your goal is to satisfy one of the following three conditions:

- Every letter in a is strictly less than every letter in b in the alphabet.
- Every letter in b is strictly less than every letter in a in the alphabet.
- Both a and b consist of only one distinct letter.

Return the minimum number of operations needed to achieve your goal.

**Example 1:**

```
Input: a = "aba", b = "caa"
Output: 2
Explanation: Consider the best way to make each condition true:
1) Change b to "ccc" in 2 operations, then every letter in a is less than every letter in b.
2) Change a to "bbb" and b to "aaa" in 3 operations, then every letter in b is less than every letter in a.
3) Change a to "aaa" and b to "aaa" in 2 operations, then a and b consist of one distinct letter.
The best way was done in 2 operations (either condition 1 or condition 3).
```

**Example 2:**

```
Input: a = "dabadd", b = "cda"
Output: 3
Explanation: The best way is to make condition 1 true by changing b to "eee".
```

**Constraints:**

- 1 <= a.length, b.length <= 10<sup>5</sup>
- a and b consist only of lowercase letters.

******************************
**Explanation**
- since the string only consists of lowercase letters, use an array of length 26 to count the frequency of each letter
- for condition 1, the minimum operation will be sum(db[:i]) + sum(da[i:]) where i is the chosen splitting point
  - replace all the letters below i to a letter that is higher than i in b
  - replace all the letters above i to a letter that is lower than i in a
- for condition 2, the minimum operation will be sum(da[:i]) + sum(db[i:]) 
- use prefix sum to store the partial sum (reduce time complexity)
- for condition 3, the minimum operation will be len(a) - the number of the most frequent letter in a + len(b) - the number of the most frequent letter in b
- return the minimum from the above three conditions

**Python**

```python
class Solution:
    class Solution:
    def minCharacters(self, a: str, b: str) -> int:
        def getDict(s):
            d = [0 for _ in range(26)]
            for ch in s:
                d[ord(ch)-ord("a")] += 1
            return d
        
        def getPrefixSum(l):
            ret = [0 for _ in range(len(l))]
            if l:
                ret[0] = l[0]
            for i in range(1, len(l)):
                ret[i] = ret[i-1] + l[i]
            return ret
         
        da = getDict(a)
        db = getDict(b)
        
        daSum = getPrefixSum(da)
        dbSum = getPrefixSum(db)
                
        ans = math.inf
        
        for i in range(1, 26): 
            ans = min(ans, daSum[i-1] + dbSum[-1] - dbSum[i-1], dbSum[i-1] + daSum[-1] - daSum[i-1])
        
        return min(ans, len(a) - max(da) + len(b) - max(db))
```

**Complexity**:

- Time Complexity: ```O(max(Na, Nb))``` where Na is the length of the string a and Nb is the length of the string b.
- Space Complexity: ```O(1)```
