### Leetcode297. [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.


Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.


Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg) 

Input: root = [1,2,3,null,null,4,5]\
Output: [1,2,3,null,null,4,5]

**Example 2:**

Input: root = []\
Output: []

**Example 3:**

Input: root = [1]\
Output: [1]


**Example 4:**

Input: root = [1,2]\
Output: [1,2]

**Constraints:**

- The number of nodes in the tree is in the range [0, 10<sup>4</sup>].
- -1000 <= Node.val <= 1000

******************************
**Explanation**
- Traverse the tree and encoded into string in preorder. When the node itself is NULL, encode 'NULL'.
- Follow the same preorder traverse to decode the string, and build the tree recusively.
  
**Python**

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        # preorder
        if not root:
            return "null,"
        return str(root.val) + "," + self.serialize(root.left) + self.serialize(root.right)

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        node = data.split(",")
        def preorder(i):
            if i > len(node) or node[i] == "null":
                return i, None
            
            root = TreeNode(int(node[i]))
            j, root.left = preorder(i+1)
            k, root.right = preorder(j+1)
            return k, root
            
        return preorder(0)[1]
        

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))

```

**Complexity**

- Time Complexity: ```O(N)```
- Space Complexity: ```O(H)``` where H is the height of the tree
