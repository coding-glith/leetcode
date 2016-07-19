# Minimum Path Sum

> Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

> Note: You can only move either down or right at any point in time.

```Python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m = len(grid)
        n = len(grid[0])
        pathSum = [[0 for col in range(n)] for row in range(m)]
        pathSum[0][0] = grid[0][0]
        for row in range(1, m):
            pathSum[row][0] = pathSum[row-1][0] + grid[row][0]
        for col in range(1, n):
            pathSum[0][col] = pathSum[0][col-1] + grid[0][col]
        for row in range(1, m):
            for col in range(1, n):
                pathSum[row][col] = min(pathSum[row-1][col], pathSum[row][col-1]) + grid[row][col]
        return pathSum[m-1][n-1]
```
