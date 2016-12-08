# Shortest Path to Escape Maze

> In a maze, where 1 represents a wall that cannot go through, 0, represents floors that can use

> Give the position of the exit, and (0, 0) is the starting point.

> Return the shortest distance to escape the maze, if no path, return -1.

> Example,

> ```
[
  [0, 0, 0, 0], 
  [1, 0, 1, 0],
  [1, 0, 0, 0]
]
return 2 if exit at (1, 1)
return 4 if exit at (1, 3)
```

The idea is to start at the exit, use BFS to update its neighbor's distance to the exit.

```Python
class Solution(object):
    def shortestMazePath(self, maze, exitRow, exitCol):
        """
        :type maze: [[int]]
        :type exitRow, exitCol: int
        :rtype: int
        """
        if not maze: return -1
        queue = collections.deque([(exitRow, exitCol, 0)])
        dp = [[0] * len(maze[0]) for _ in xrange(len(maze))]
        visited = [[False] * len(maze[0]) for _ in xrange(len(maze))]
        while queue:
            x, y, path = queue.popleft()
            visited[x][y] = True
            for i, j in ((x+1, y), (x-1, y), (x, y+1), (x, y-1)):
                if 0 <= i < len(maze) and 0 <= j < len(maze[0]) and dp[i][j] != -1 and not visited[i][j]:
                    if maze[i][j] == 1:
                        dp[i][j], visited[i][j] = -1, True
                    else:
                        dp[i][j] = min(dp[i][j], path+ 1) if dp[i][j] != 0 else path + 1
                        queue.append((i, j, dp[i][j]))
        for i in xrange(len(maze)):
            for j in xrange(len(maze[0])):
                if i != exitRow or j != exitCol and dp[i][j] == 0: dp[i][j] = -1
        return dp[0][0]
```
