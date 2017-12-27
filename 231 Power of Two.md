Problem Description
-------------------

Given an integer, write a function to determine if it is a power of two.

Tip
---

Bit Operation

(1) not n & (n-1): `​O(1)`

(2) 轉換Bit to String

 ‘{:b}’.format(n)

 str( bin( n ) )

 計算 char 個數 .count( char )

##Solution
```python
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        return not (n & (n-1)) and n > 0
```