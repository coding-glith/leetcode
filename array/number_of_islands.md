# Number of Islands

> Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

> Example 1:

> ```
11110
11010
11000
00000
Answer: 1
```

> Example 2:

> ```
11000
11000
00100
00011
Answer: 3
```

DFS.

```Python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not grid[0]: return 0
        res, visited = 0, [[False] * len(grid[0]) for _ in xrange(len(grid))]
        for row in xrange(len(grid)):
            for col in xrange(len(grid[row])):
                if grid[row][col] == "1" and not visited[row][col]:
                    self.dfs(grid, visited, row, col)
                    res += 1
        return res

    def dfs(self, grid, visited, row, col):
        if row < 0 or row >= len(grid) or col < 0 or col >= len(grid[0]) \
           or grid[row][col] != '1' or visited[row][col]:
            return
        visited[row][col] = True
        self.dfs(grid, visited, row-1, col)
        self.dfs(grid, visited, row+1, col)
        self.dfs(grid, visited, row, col-1)
        self.dfs(grid, visited, row, col+1)
```

BFS.

```Python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not grid[0]: return 0
        res, visited = 0, [[False] * len(grid[0]) for _ in xrange(len(grid))]

        for row in xrange(len(grid)):
            for col in xrange(len(grid[row])):
                if grid[row][col] == "1" and not visited[row][col]:
                    self.bfs(grid, visited, row, col)
                    res += 1
        print grid, visited
        return res

    def bfs(self, grid, visited, row, col):
        queue = collections.deque([(row, col)])
        while queue:
            x, y = queue.popleft()
            for i, j in [(x-1, y), (x+1, y), (x, y-1), (x, y+1)]:
                if 0 <= i < len(grid) and 0 <= j < len(grid[0]) and not visited[i][j]:
                    if grid[i][j] == '1':
                        visited[i][j] = True
                        queue.append((i, j))
```
