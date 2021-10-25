### Leetcode 76. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

A substring is a contiguous sequence of characters within the string.

**Example 1:**

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

**Example 2:**

```
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
```

**Example 3:**

```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```

**Constraints:**

- m == s.length
- n == t.length
- 1 <= m, n <= 10<sup>5</sup>
- s and t consist of uppercase and lowercase English letters.

******************************
**Explanation**
- first, use a hashmap to count the letters in t
- sliding window on the string s
  - keep a hashmap of the sliding window
  - keep the count of required letters in t (required) and the count of already matched letters in s (formed)
  - in each step, update the current window and check if the conditions are satisfied
  - then move the left pointer to move forward until the conditions are not satisfied again

**Python**

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        
        d = defaultdict(int)
        for ch in t:
            d[ch] += 1
        
        window = defaultdict(int)
        start = 0
        minValue = math.inf
        pos = -1
        formed, required = 0, len(d)
        for i in range(len(s)):
            curr = s[i]
            window[curr] += 1
            if curr in d and window[curr] == d[curr]:
                formed += 1
            while start <= i and formed == required:
                if minValue > i - start + 1:
                    minValue = i - start + 1
                    pos = start
                window[s[start]] -= 1
                if s[start] in d and window[s[start]] < d[s[start]]:
                    formed -= 1
                start += 1

        return s[pos: pos+minValue] if pos != -1 else ""
```

**Complexity**:

- Time Complexity: ```O(m + n)``` where m is the length of s and n is the length of t
- Space Complexity: ```O(m + n)``` 
