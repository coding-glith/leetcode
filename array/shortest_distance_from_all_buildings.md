# Shortest Distance from All Buildings

> You want to build a house on an empty land which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values 0, 1 or 2, where:

> * Each 0 marks an empty land which you can pass by freely.

> * Each 1 marks a building which you cannot pass through.

> * Each 2 marks an obstacle which you cannot pass through.

> For example, given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2):

> ```
1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0
```

> The point (1,2) is an ideal empty land to build a house, as the total travel distance of 3+3+1=7 is minimal. So return 7.

> Note:

> * There will be at least one building. If it is not possible to build such house according to the above rules, return -1.

BFS.

```Python
class Solution(object):
    def shortestDistance(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if not grid or not grid[0]: return -1
        rowNum, colNum = len(grid), len(grid[0])
        totalBuildings = sum(val for row in grid for val in row if val == 1)
        # hit marks the total buildings an empty space can reach
        hit = [[0] * colNum for row in xrange(rowNum)]
        # distSum is the total distance the empty space reaches each building
        distSum = [[0] * colNum for row in xrange(rowNum)]

        def bfs(row, col):
            visited = [[False] * colNum for _ in xrange(rowNum)]
            visited[row][col], countBuildings = True, 1
            queue = collections.deque([(row, col, 0)])
            while queue:
                x, y, distance = queue.popleft()
                for i, j in [(x+1, y), (x-1, y), (x, y+1), (x, y-1)]:
                    if 0 <= i < rowNum and 0 <= j < colNum and not visited[i][j]:
                        visited[i][j] = True
                        if grid[i][j] == 0:
                            queue.append((i, j, distance + 1))
                            hit[i][j] += 1
                            distSum[i][j] += distance + 1
                        if grid[i][j] == 1:
                            countBuildings += 1
            return countBuildings == totalBuildings

        # build hit and distSum
        for row in xrange(rowNum):
            for col in xrange(colNum):
                # for each building, do bfs to find the distance to each empty space
                if grid[row][col] == 1:
                    if not bfs(row, col): return -1

        # go through distSum to find the minimum
        return min([distSum[i][j] for i in xrange(rowNum) for j in xrange(colNum) if grid[i][j] == 0 and hit[i][j] == totalBuildings] or [-1])

```
