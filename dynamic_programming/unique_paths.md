# Unique Paths

> A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

> The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

> How many possible unique paths are there?

> ![alt text](http://leetcode.com/wp-content/uploads/2014/12/robot_maze.png)

> Above is a 3 x 7 grid. How many possible unique paths are there?

> Note: m and n will be at most 100.

```Python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        if m <= 0 or n <= 0:
            return 0
        pathNum = [[0 for col in range(n)] for row in range(m)]
        for row in range(m):
            pathNum[row][0] = 1
        for col in range(n):
            pathNum[0][col] = 1
        for row in xrange(1, m):
            for col in xrange(1, n):
                pathNum[row][col] = pathNum[row-1][col] + pathNum[row][col-1]
        return pathNum[m-1][n-1]
```

# Unique Paths II

> Follow up for "Unique Paths":

> Now consider if some obstacles are added to the grids. How many unique paths would there be?

> An obstacle and empty space is marked as 1 and 0 respectively in the grid.

> For example,

> There is one obstacle in the middle of a 3x3 grid as illustrated below.

> ```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

> The total number of unique paths is 2.

> Note: m and n will be at most 100.

```Python

```
