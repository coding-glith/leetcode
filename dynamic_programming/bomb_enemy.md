# Bomb Enemy

> Given a 2D grid, each cell is either a wall 'W', an enemy 'E' or empty '0' (the number zero), return the maximum enemies you can kill using one bomb.
The bomb kills all the enemies in the same row and column from the planted point until it hits the wall since the wall is too strong to be destroyed.
Note that you can only put the bomb at an empty cell.

> Example:

> ```
For the given grid
0 E 0 0
E 0 W E
0 E 0 0
return 3. (Placing a bomb at (1,1) kills 3 enemies)
```

The idea is to reuse the rowhits and colhits. Only recalculate them when meet a wall.

```Python
class Solution(object):
    def maxKilledEnemies(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid: return 0
        res = 0
        colhits = [0] * len(grid[0])
        for i, row in enumerate(grid):
            for j, cell in enumerate(row):
                if j == 0 or row[j-1] == 'W': # only recaculate when meet wall
                    rowhits = 0
                    for k in xrange(j, len(grid[0])):
                        if row[k] == 'W': break
                        rowhits += row[k] == 'E'
                if i == 0 or grid[i-1][j] == 'W':
                    colhits[j] = 0
                    for k in xrange(i, len(grid)):
                        if grid[k][j] == 'W': break
                        colhits[j] += grid[k][j] == 'E'
                if cell == '0':
                    res = max(res, rowhits + colhits[j])
        return res
```
