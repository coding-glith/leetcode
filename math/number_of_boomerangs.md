# Number of Boomerangs

> Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

> Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range [-10000, 10000] (inclusive).

> Example:

> ```
Input:
[[0,0],[1,0],[2,0]]
Output:
2
Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

```Python
class Solution(object):
    def numberOfBoomerangs(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        if not points: return 0
        res = 0
        for i, point in enumerate(points):
            distanceDict = {}
            for j, p in enumerate(points):
                if j != i and p != point:
                    distanceSquare = (point[0] - p[0]) * (point[0] - p[0]) + (point[1] - p[1]) * (point[1] - p[1])
                    if distanceSquare not in distanceDict:
                        distanceDict[distanceSquare] = [p]
                    else: distanceDict[distanceSquare].append(p)
            for key in distanceDict:
                if len(distanceDict[key]) > 1:
                    n = len(distanceDict[key])
                    res += n * (n-1)
        return res
```
