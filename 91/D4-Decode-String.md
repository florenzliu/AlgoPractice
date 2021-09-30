### Leetcode 394. [Decode String](https://leetcode.com/problems/decode-string/)

Given an encoded string, return its decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

 

**Example 1:**

Input: s = "3[a]2[bc]"\
Output: "aaabcbc"

**Example 2:**

Input: s = "3[a2[c]]"\
Output: "accaccacc"

**Example 3:**

Input: s = "2[abc]3[cd]ef"\
Output: "abcabccdcdcdef"

**Example 4:**

Input: s = "abc3[cd]xyz"\
Output: "abccdcdcdxyz"\
 

**Constraints:**

- 1 <= s.length <= 30
- s consists of lowercase English letters, digits, and square brackets '[]'.
- s is guaranteed to be a valid input.
- All the integers in s are in the range [1, 300].

******************************
**Explanation**
- Use a stack to keep track of the traversed string in the square bracket and its repeated times.
- When encountering ']', pop the elements from the stack to compose the current traversed string in the current square bracket, and continue to pop in order to find its repeated times. Compose the current string and add it back to the stack.
- Join all the strings in the stack to return the final decoded string

**Python**

```python
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []
        for ch in s:
            if ch == "]":
                curr = ""
                while stack[-1] != "[":
                    curr = stack.pop() + curr
                stack.pop()
                num = ""
                while stack and stack[-1].isdigit():
                    num = stack.pop() + num
                currStr = curr * int(num)
                stack.append(currStr)
            else:
                stack.append(ch)    
        return "".join(stack)
```

**Complexity**

- Time Complexity: ```O(N)``` 
- Space Complexity: ```O(N)``` 
