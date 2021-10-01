### Leetcode 30. [Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)
You are given a string s and an array of strings words of the same length. Return all starting indices of substring(s) in s that is a concatenation of each word in words exactly once, in any order, and without any intervening characters.

You can return the answer in any order.

**Example 1:**

```
Input: s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```

**Example 2:**

```
Input: s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
Output: []
```
**Example 3:**

```
Input: s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
Output: [6,9,12]
```

**Constraints:**

- 1 <= s.length <= 10<sup>4</sup>
- s consists of lower-case English letters.
- 1 <= words.length <= 5000
- 1 <= words[i].length <= 30
- words[i] consists of lower-case English letters.

******************************
**Explanation**
- use a hashmap of words to store all the substrings
- traverse s, at each index, go from i to i + len(words) * len(words[0]), use a copy of a hashmap of words to keep track of the substrings
- use a flag to indicate whether the map has been matched completely or the loop terminates early

**Python**

```python
class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        
        d = defaultdict(int)
        n = len(words)
        wordLength = len(words[0])
        for w in words:
            d[w] += 1
        
        result = []
        for i in range(len(s)-n*wordLength+1): # range: +1
            currD = d.copy()
               
            flag = True
            for j in range(i, i+n*wordLength, wordLength):
                if s[j:j+wordLength] not in currD:
                    flag = False
                    break
                else:
                    if currD[s[j:j+wordLength]] == 0:
                        flag = False
                        break
                    else:
                        currD[s[j:j+wordLength]] -= 1
            if flag:
                result.append(i)
        return result 
```

**Complexity**:

- Time Complexity: ```O(N * m * l)``` where N is the length of s, m is the length of the words list and l is the length of each word
- Space Complexity: ```O(m)``` 
