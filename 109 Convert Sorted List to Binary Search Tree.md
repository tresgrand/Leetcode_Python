Problem Description
-------------------

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

Example:

    Given the sorted linked list: [-10,-3,0,5,9],

    One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

          0
         / \
       -3   9
       /   /
     -10  5

Tip
---

* Recursively find left child and right child
  * 要特別注意找left child & right child 遇到的終止條件
    * Left會遇到: [head] -\> None
      * 要另外判別head.next是否是None
    * Right直接會遇到: None
* Linked list 找中點的方法: slow, fast
  * 要特別記下slow的前一個node(prev)

Solution
--------

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        if not head:
            return None
        
        if not head.next:
            return TreeNode(head.val)
        
        # find the mid of LinkedList
        slow = fast = prev = head
        
        while slow and fast and fast.next:
            prev = slow
            slow = slow.next
            fast = fast.next.next
        # mid found, cut left tree
        prev.next = None
        
        root = TreeNode(slow.val)
        
        root.left = self.sortedListToBST(head)
        root.right = self.sortedListToBST(slow.next)
        return root
```