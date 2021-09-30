### Leetcode 3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
Given a string s, find the length of the longest substring without repeating characters.

**Example 1:**

```
Input: s = "abcabcbb"\
Output: 3\
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
**Example 3:**

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Example 4:**

```
Input: s = ""
Output: 0
```

**Constraints:**

- 0 <= s.length <= 5 * 10<sup>4</sup>
- s consists of English letters, digits, symbols and spaces.

******************************
**Explanation**
- use sliding window, within which there is no repetitive numbers
- use a hashset to store all the traversed numbers in the sliding window
- use maxLength to store the current max length

**Python**

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left = 0 
        maxLen = 0
        h = set()
        for i in range(len(s)):
            if s[i] not in h:
                h.add(s[i])
                maxLen = max(maxLen, i-left+1)
            else:
                while s[i] in h:
                    h.remove(s[left])
                    left += 1
                h.add(s[i])
        return maxLen  
```

**Complexity**:

- Time Complexity: O(N)
- Space Complexity: O(N)
