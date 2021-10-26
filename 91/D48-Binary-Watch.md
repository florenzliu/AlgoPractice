### Leetcode 401. [Binary Watch](https://leetcode.com/problems/binary-watch/)
A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59). Each LED represents a zero or one, with the least significant bit on the right.

- For example, the below binary watch reads "4:51".

![](https://assets.leetcode.com/uploads/2021/04/08/binarywatch.jpg?)

Given an integer turnedOn which represents the number of LEDs that are currently on, return all possible times the watch could represent. You may return the answer in any order.

The hour must not contain a leading zero.

- For example, "01:00" is not valid. It should be "1:00".

The minute must be consist of two digits and may contain a leading zero.

- For example, "10:2" is not valid. It should be "10:02".

**Example 1:**

```
Input: turnedOn = 1
Output: ["0:01","0:02","0:04","0:08","0:16","0:32","1:00","2:00","4:00","8:00"]
```

**Example 2:**

```
Input: turnedOn = 9
Output: []
```

**Constraints:**

- 0 <= turnedOn <= 10

******************************
**Explanation**
- approach 1: permutation problem using dfs/backtracking
- bit manipulation: hr < 12, minute < 60

**Python**

```python
# Approach 1
class Solution:
    def readBinaryWatch(self, turnedOn: int) -> List[str]:
        group = [8, 4, 2, 1, 32, 16, 8, 4, 2, 1]
        res = []
        
        def dfs(hour, minute, n, index, group):
            # base case:
            if hour >= 12 or minute >= 60:
                return
            if n == 0:
                zero = "0" if minute < 10 else ""
                time = str(hour) + ":" + zero + str(minute)
                res.append(time)
                return
            
            if index < len(group):
                if index <= 3: # handle hours
                    dfs(hour + group[index], minute, n-1, index+1, group)
                else: # handle minutes
                    dfs(hour, minute + group[index], n-1, index+1, group)
                dfs(hour, minute, n, index+1, group)

        
        dfs(0, 0, turnedOn, 0, group)

        return res

# Approach 2
class Solution:
    def readBinaryWatch(self, turnedOn: int) -> List[str]:
        res = []
        for h in range(12):
            for m in range(60):
                if (bin(h) + bin(m)).count("1") == turnedOn:
                    zero = "0" if m < 10 else ""
                    time = str(h) + ":" + zero + str(m)
                    res.append(time)
        return res

```

**Complexity**:

- Time Complexity: ```O(1)```
- Space Complexity: ```O(1)```
