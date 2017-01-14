# Meeting Rooms

> Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

> For example,

> Given [[0, 30],[5, 10],[15, 20]],

> return false.

```Python
# Definition for an interval.
# class Interval(object):
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution(object):
    def canAttendMeetings(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: bool
        """
        intervals.sort(key=lambda x: x.start)
        for i in xrange(1,len(intervals)):
            if intervals[i].start < intervals[i-1].end:
                return False
        return True
```

# Meeting Rooms II

> Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

> For example,

> ```
Given [[0, 30],[5, 10],[15, 20]],
return 2.
```

Check from leetcode [discussion](https://discuss.leetcode.com/topic/20912/my-python-solution-with-explanation). The idea is to maintain sorted start, end array, whenever we want to start a new meeting, check if previous meeting ends, if ends, available meeting room +1. if not, check whether need to start a new meeting room or use current availabe meeting room.

```Python
# Definition for an interval.
# class Interval(object):
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution(object):
    def minMeetingRooms(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: int
        """
        start = sorted(i.start for i in intervals)
        end = sorted(j.end for j in intervals)
        numRoom, available, s, e = 0, 0, 0, 0
        while s < len(start):
            if start[s] < end[e]:
                if available == 0:
                    numRoom += 1
                else:
                    available -= 1
                s += 1
            else:
                available += 1
                e += 1
        return numRoom
```
