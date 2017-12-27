Problem Description
-------------------

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples: 

`[2,3,4]` , the median is `3`

`[2,3]`, the median is `(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

* void addNum(int num) - Add a integer number from the data stream to the data structure.
* double findMedian() - Return the median of all elements so far.

For example:

    addNum(1)
    addNum(2)
    findMedian() -> 1.5
    addNum(3) 
    findMedian() -> 2

Tip
---

用list存會超時

用兩個heap做: small(max heap), large(min heap)

 large - small \<= 1 

 len == odd: 回傳large, len == even: 回傳 large + small /2\.

Solution
--------

```python
class MedianFinder(object):

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.small = [] # max heap
        self.large = [] # min heap

    def addNum(self, num):
        """
        :type num: int
        :rtype: void
        """
        # push num into small -> pop the biggest from small -> push to large
        heapq.heappush(self.large, -heapq.heappushpop(self.small, -num))
        # large heap should always one ele more or equal to small heap
        if len(self.large) - len(self.small) > 1:
            heapq.heappush(self.small, -heapq.heappop(self.large))
    def findMedian(self):
        """
        :rtype: float
        """
        if len(self.large) > len(self.small):
            return float(self.large[0])
        return (self.large[0] - self.small[0]) / 2.
```