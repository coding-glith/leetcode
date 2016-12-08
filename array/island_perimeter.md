# Island Perimeter

> You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

> Example:

> ```
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]
Answer: 16
```

```Python
class Solution(object):
    def islandPerimeter(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        res = 0
        for i, row in enumerate(grid):
            for j, val in enumerate(row):
                if val == 1:
                    for x, y in ((i+1, j), (i-1, j), (i, j+1), (i, j-1)):
                        if 0 <= x < len(grid) and 0 <= y < len(grid[0]) and grid[x][y] == 1: continue
                        res += 1
        return res
```
