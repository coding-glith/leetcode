# Merge Intervals

> Given a collection of intervals, merge all overlapping intervals.

> For example,

> ```
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].
```

```Python
# Definition for an interval.
# class Interval(object):
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution(object):
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        intervals.sort(key=lambda x:x.start)
        result, idx = [], 0
        while idx < len(intervals):
            sub, i = [intervals[idx].start, intervals[idx].end], idx + 1
            while i < len(intervals):
                if sub[1] < intervals[i].start: break
                sub[1] = max(sub[1], intervals[i].end)
                i += 1
            result.append(list(sub))
            idx = i
        return result
```
