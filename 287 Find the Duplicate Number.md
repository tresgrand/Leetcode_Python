Problem Description
-------------------

Given an array *nums* containing *n* + 1 integers where each integer is between 1 and *n* (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

Note:

1. You must not modify the array (assume the array is read only).
2. You must use only constant, *O*(1) extra space.
3. Your runtime complexity should be less than `O(n2)`.
4. There is only one duplicate number in the array, but it could be repeated more than once.

Tip
---

要把它看成 Cycle linked list 題目解

duplicate number即是cycle起始點

1. ​​先找出bump的點
2. 再找cycle begin的點(即duplicate)
  1. start到cycle begin的距離＝bomp到cycle begin的距離

![](resources/7A28762448ABE4C71B7AE82D19710EEC.jpg =300x)

##Solution
```python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) < 2:
            return None
        if len(nums) == 2:
            return nums[0]
        
        slow = nums[nums[0]]
        fast = nums[nums[nums[0]]]
        # find meet point
        while slow != fast:
            slow = nums[slow]
            fast = nums[nums[fast]]
        
        # meet point -> cycle begin == start point -> cycle begin
        # cycle begin == duplicate number
        slow = nums[0]
        while slow != fast:
            slow = nums[slow]
            fast = nums[fast]
        
        return slow
```

