# Longest Consecutive Sequence

> Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

> For example,

> Given [100, 4, 200, 1, 3, 2],

> The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

> Your algorithm should run in O(n) complexity.

This solution takes the advantage of using set(), where the "in" operation is O(1) in average.

Check the time complexity at [wiki](https://wiki.python.org/moin/TimeComplexity).

```Python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        tmp = set(nums)
        res = 0
        while tmp:
            start = end = tmp.pop()
            while start - 1 in tmp:
                start -= 1
                tmp.remove(start)
            while end + 1 in tmp:
                end += 1
                tmp.remove(end)
            res = max(res, end + 1 - start)
        return res
```
