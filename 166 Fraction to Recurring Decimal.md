Problem Description
-------------------

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

For example,

* Given numerator = 1, denominator = 2, return "0.5".
* Given numerator = 2, denominator = 1, return "2".
* Given numerator = 2, denominator = 3, return "0.(6)".

Tip
---

* 分成三部分:
  1. 正負:
    * 決定要不要append ‘-‘
  2. 商 Quotient part
    * append 商
  3. 餘 Remainder part
    * 用一個 dict 紀錄出現過的`餘數`以及`對應的位置`
    * 當再重複出現的話 直接insert ( ) break while loop
* 也可用stack
  * <https://discuss.leetcode.com/topic/7699/do-not-use-python-as-cpp-here-s-a-short-version-python-code>

Solution
--------

```python
class Solution(object):
    def fractionToDecimal(self, numerator, denominator):
        """
        :type numerator: int
        :type denominator: int
        :rtype: str
        """
        if not numerator: # or if numerator == 0:
            return '0'
        
        res = []
        dct = {}
        
        # +-
        if numerator * denominator < 0:
            res.append('-')
        
        numer, denom = abs(numerator), abs(denominator)
        n, remainder = divmod(numer, denom)
        
        # quotient part
        res.append(str(n))
        if remainder == 0:
            return ''.join(res)
        
        # fraction part
        res.append('.')
        while remainder != 0:
            if dct.get(remainder):
                res.insert(dct[remainder], '(')
                res.append(')')
                break
            dct[remainder] = len(res)
            remainder *= 10
            res.append(str(remainder / denom)) # calculate divide
            remainder %= denom # update remainder

        return ''.join(res)
```