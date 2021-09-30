# Chap 1. Array, Stack, Queue

## Array

#### Time Complexity Analysis

| Type | Insert | Delete | Update | Search | Traverse |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Array | O\(n\) | O\(n\) | O\(1\) | O\(1\) | O\(n\) |

#### Operations

* each\(\): traverse
* pop\(index\): delete element by its index
* insert\(item, index\): insert item at index

#### Practice Questions

* Easy

LC 414. [Third Maximum Number](https://leetcode.com/problems/third-maximum-number/)

LC 859. [Buddy Strings](https://leetcode.com/problems/buddy-strings/)

* Medium

LC 88. [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

LC 59. [Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/)

LC 380. [Insert Delete GetRandom O\(1\)](https://leetcode.com/problems/insert-delete-getrandom-o1/)

* Hard

LC 41. [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) 

## Stack

#### 

#### Time Complexity Analysis

| Type | Push | Pop | Top |
| :--- | :--- | :--- | :--- |
| Stack | O\(1\) | O\(1\) | O\(1\) |

#### Application

* function call
* web browser backward
* bracket matching
* monotonic stack \(find next larger/smaller element\)
* calculator
* DFS

#### Practice Questions

* Medium

LC 150. [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

LC 1381. [Design a Stack With Increment Operation](https://leetcode.com/problems/design-a-stack-with-increment-operation/)

LC 394. [Decode String](https://leetcode.com/problems/decode-string/)

LC 946. [Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/)

LC 227. [Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/)

LC 20. [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

## Queue

#### Time Complexity Analysis

| Type | Insert | Delete | Peek |
| :--- | :--- | :--- | :--- |
| Queue \(LinkedList\) | O\(1\) | O\(1\) | O\(1\) |
| Queue \(List\) | O\(n\) | O\(n\) | O\(1\) |

#### Application

* BFS

#### Practice Questions

* Easy

LC 155. [Min Stack](https://leetcode.com/problems/min-stack/)

LC 94. [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

LC 232. [Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)

* Medium

LC 133. [Clone Graph](https://leetcode.com/problems/clone-graph/)

LC 200. [Number of Islands](https://leetcode.com/problems/number-of-islands/)

LC 542. [01 Matrix](https://leetcode.com/problems/01-matrix/)

* Hard

LC 84. [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

## Bucket & Counting

#### Practice Questions

* Medium

LC 49. [Group Anagrams](https://leetcode.com/problems/group-anagrams/)

LC 825. [Friends Of Appropriate Ages](https://leetcode.com/problems/friends-of-appropriate-ages/)

Interview Question: [Largest Range](https://github.com/azl397985856/leetcode/issues/420)

