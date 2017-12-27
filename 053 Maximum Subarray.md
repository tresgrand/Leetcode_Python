Problem Description
-------------------

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array `[-2,1,-3,4,-1,2,1,-5,4]`,
the contiguous subarray `[4,-1,2,1]` has the largest sum = `6`.

Tip
---

Dynamic programming

存一個max 存一個dp

## Solution
```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return None
        # opt: max subarray from 0 to i
        # maxVal: max subarray
        opt = maxVal = nums[0]
        
        for i, ele in enumerate(nums[1:], 1):
            opt = max(opt + ele, ele)
            maxVal = max(opt, maxVal)
                
            
        return maxVal
```