Problem Description
-------------------

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

Note: Do not modify the linked list.

Follow up:
Can you solve it without using extra space?

##Tip
可證得start->cycle begin == bump->cycle begin
![](resources/0AFEEF186F3C37271F4BFEC1BFF4F3CC.jpg =300x)
##Solution
```python
class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return None
        
        slow = fast = head
        
        # find bomp
        while slow and fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                slow = head
                # find begin
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        
        return None
```