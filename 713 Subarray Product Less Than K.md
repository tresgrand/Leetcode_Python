Problem Description
-------------------

Your are given an array of positive integers `nums`.

Count and print the number of (contiguous) subarrays where the product of all the elements in the subarray is less than `k`.

Example 1:

    Input: nums = [10, 5, 2, 6], k = 100
    Output: 8
    Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
    Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

Note:

* `0 < nums.length <= 50000`.
* `0 < nums[i] < 1000`.
* `0 <= k < 10^6`.

Tip
---

1. 用Sliding window 解: O(n)
  1. [ ]
  2. ^ ^
2. 用two pointer跑兩個for loop: O(n2) -\> **TLE**

Solution
--------

```python
# sliding window
class Solution(object):
  def numSubarrayProductLessThanK(self, nums, k):
    '''
    type nums: List[int]
    type k: int
    rtype: int
    '''
    res = 0
    curProd = 1
    left = 0
    for i in range(len(nums)):
      curProd *= nums[i]
      while curProd >= k and left <= i:
        curProd /= nums[left]
        left += 1
      res += (i - left + 1)
    return res
```

**Time Limit Exceed**

```python
# nested for-loop
# TIME LIMIT EXCEEDED
class Solution(object):
  def numSubarrayProductLessThanK(self, nums, k):
    '''
    type nums: List[int]
    type k: int
    rtype: int
    '''
    ans = 0
    for i in range(len(nums)):
      cur = nums[i]
      if nums[i] >= k:
        continue
      
      ans+=1
      
      for j in range(i+1, len(nums)):
        cur *= nums[j]
        if cur >= k:
          break
        ans+=1
    return ans
```