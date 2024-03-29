# Insert Interval

> Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

> You may assume that the intervals were initially sorted according to their start times.

> Example 1:

> Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].

> Example 2:

> Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

> This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

construct the left, right and merge part during the way of traversing the list.

```Python
# Definition for an interval.
# class Interval(object):
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution(object):
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        startVal, endVal = newInterval.start, newInterval.end
        left, right = [], []
        for val in intervals:
            if val.end < startVal:
                left += [val]
            elif val.start > endVal:
                right += [val]
            else:
                startVal = min(startVal, val.start)
                endVal = max(endVal, val.end)
        return left + [Interval(startVal, endVal)] + right
```

when meeting val.end >= newInterval.start, cases to be consider:

> * insert before current interval

> * merge with current interval, update both start and end

> * check if merged the interval or not at the very end

```Python
# Definition for an interval.
# class Interval(object):
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution(object):
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        result, flag = [], False
        for val in intervals:
            if not result or val.start > result[-1].end:
                result.append(val)
            else:
                result[-1].end = max(result[-1].end, val.end)
            if not flag and val.end >= newInterval.start:
                flag = True
                if newInterval.end < val.start:
                    result.insert(-1, newInterval)
                else:
                    result[-1].start = min(result[-1].start, newInterval.start)
                    result[-1].end = max(result[-1].end, newInterval.end)
        return result if flag else result + [newInterval]
```
