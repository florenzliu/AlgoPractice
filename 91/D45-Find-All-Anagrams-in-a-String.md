### Leetcode 438. [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```
Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

**Constraints:**

- 1 <= s.length, p.length <= 3 * 10<sup>4</sup>
- s and p consist of lowercase English letters.

******************************
**Explanation**
- since s and p contains only lower case letters, use an array as a hashmap to count the letters 
- sliding window on the string s

**Python**

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        d = [0 for _ in range(26)]
        for ch in p:
            index = ord(ch) - ord("a")
            d[index] += 1
        
        t = [0 for _ in range(26)]
        output = []
        n = len(p)
        for i in range(len(s)):
            t[ord(s[i]) - ord('a')] += 1
            if i >= n:
                t[ord(s[i - n]) - ord('a')] -= 1
            if t == d:
                output.append(i - n + 1)
        
        return output
```

**Complexity**:

- Time Complexity: ```O(N)```
- Space Complexity: ```O(1)```
