Problem Description
-------------------

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

        1
       / \
      2   2
     / \ / \
    3  4 4  3

But the following `[1,2,2,null,3,null,3]` is not:

        1
       / \
      2   2
       \   \
       3    3

Note:
Bonus points if you could solve it both recursively and iteratively

Tip
---

1. 建一個比對兩個node是否相等的function (就只要比對 (1) L.val == R.val or (2) L.None == R.None)
  1. 關鍵在於每次丟進去兩個node的方法(Symmetric的丟)
2. 用 Stack (沒試)

Solution
--------

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        
        return self.isIdentical(root.left, root.right)
    
    def isIdentical(self, left, right):
        if not left and not right:
            return True
        if not left or not right:
            return False
        
        if left.val == right.val:
            return self.isIdentical(left.left, right.right) and self.isIdentical(left.right, right.left)
        else:
            return False
```