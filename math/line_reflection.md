# Line Reflection

> Given n points on a 2D plane, find if there is such a line parallel to y-axis that reflect the given points.

> Example 1:

> Given points = [[1,1],[-1,1]], return true.

> Example 2:

> Given points = [[1,1],[-1,-1]], return false.

> Follow up:

> Could you do better than O(n2)?

> Hint:

> * Find the smallest and largest x-value for all points.

> * If there is a line then it should be at y = (minX + maxX) / 2.

> * For each point, make sure that it has a reflected point in the opposite side.

This is to find a line that will reflect all the given points on the plane. Need to consider points overlap, sort() only based on x axis value.

```Python
class Solution(object):
    def isReflected(self, points):
        """
        :type points: List[List[int]]
        :rtype: bool
        """
        if len(points) < 2:
            return True
        points.sort()   # sort based on x-value
        line = (points[0][0] + points[-1][0] ) / 2.0
        # check each point should have a reflect point on the other side of line
        pDict = {}
        for i in xrange(len(points)):
            if points[i][1] not in pDict:
                pDict[points[i][1]] = [points[i][0]]
            else:
                pDict[points[i][1]].append(points[i][0])
        for key in pDict:
            if not self.check(pDict[key], line):
                return False
        return True

    def check(self, p, line):
        p.sort()
        start, end = 0, len(p)-1
        while start < end:
            if (p[start] + p[end]) / 2.0 != line:
                return False
            # might contain overlap points like [[-16,1],[16,1],[16,1]]
            i, j = 1, 1
            while start + i < len(p) and p[start+i] == p[start]:
                i += 1
            start += i
            while end - j > -1 and p[end-j] == p[end]:
                j += 1
            end -= j
        if start == end:
            return p[start] == line
        return True
```
