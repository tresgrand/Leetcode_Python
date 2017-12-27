Problem Description
-------------------

Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?



##Solution
```python
class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        # head == None
        if not head:
            return False
        
        slow = head
        fast = head
        
        while slow and fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```