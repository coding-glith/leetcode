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

Union Find. O(MNlogMN)

```Python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not grid[0]: return 0
        UF = UnionFind(grid)
        for i, row in enumerate(grid):
            for j, val in enumerate(row):
                if val == "1":
                    for (x, y) in ((i+1, j), (i, j+1)):
                        if 0 <= x < len(grid) and 0 <= y < len(grid[0]) and grid[x][y] == "1":
                            p, q = i * len(grid[0]) + j, x * len(grid[0]) + y
                            UF.union(p, q)
        return UF.countHead

class UnionFind(object):
    def __init__(self, grid):
        self.N = len(grid) * len(grid[0])
        self.idArray = [i for i in xrange(self.N)]
        self.sizeArray = [1] * self.N
        self.countHead = 0
        for i, row in enumerate(grid):
            for j, val in enumerate(row):
                if val == "1": self.countHead += 1

    def root(self, i):
        while self.idArray[i] != i:
            self.idArray[i] = self.idArray[self.idArray[i]]
            i = self.idArray[i]
        return i

    def connected(self, p, q):
        return self.root(p) == self.root(q)

    def union(self, p, q):
        i, j = self.root(p), self.root(q)
        if i == j: return
        if self.sizeArray[i] < self.sizeArray[j]:
            self.idArray[i] = j
            self.sizeArray[j] += self.sizeArray[i]
        else:
            self.idArray[j] = i
            self.sizeArray[i] += self.sizeArray[j]
        self.countHead -= 1
```

# Number of Islands II

> A 2d grid map of m rows and n columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

> Example:

> Given m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]].

> Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).

> ```
0 0 0
0 0 0
0 0 0
```

> Operation #1: addLand(0, 0) turns the water at grid[0][0] into a land.

> ```
1 0 0
0 0 0   Number of islands = 1
0 0 0
```

> Operation #2: addLand(0, 1) turns the water at grid[0][1] into a land.

> ```
1 1 0
0 0 0   Number of islands = 1
0 0 0
```

> Operation #3: addLand(1, 2) turns the water at grid[1][2] into a land.

> ```
1 1 0
0 0 1   Number of islands = 2
0 0 0
```

> Operation #4: addLand(2, 1) turns the water at grid[2][1] into a land.

> ```
1 1 0
0 0 1   Number of islands = 3
0 1 0
```

> We return the result as an array: [1, 1, 2, 3]

> Challenge:

> * Can you do it in time complexity O(k log mn), where k is the length of the positions?

Weighted quick-union with path compression. Refer to leetcode [discussion](https://discuss.leetcode.com/topic/29518/java-python-clear-solution-with-unionfind-class-weighting-and-path-compression). The running time for this solution is O(klogk).

```Python
class Solution(object):
    def numIslands2(self, m, n, positions):
        """
        :type m: int
        :type n: int
        :type positions: List[List[int]]
        :rtype: List[int]
        """
        res = []
        islands = Union()
        for node in map(tuple, positions):
            islands.add(node)
            for idx in (0, 1), (0, -1), (1, 0), (-1, 0):
                neighborNode = (node[0]+idx[0], node[1]+idx[1])
                if neighborNode in islands.id:
                    islands.unite(node, neighborNode)
            res += [islands.count]
        return res

class Union(object):
    def __init__(self):
        # self.id[node] keeps the parent of node
        self.id = {}
        # to avoid tall trees
        # keep track of size of each component
        # balance by linking small tree below larger one
        self.sz = {}
        self.count = 0

    def add(self, node):
        self.id[node] = node
        self.sz[node] = 1
        self.count += 1

    def root(self, node):
        # path compression to keep a really flat trees
        while self.id[node] != node:
            # from node go all the way up to the root
            self.id[node] = self.id[self.id[node]]
            node = self.id[node]
        return node

    def unite(self, node, neighborNode):
        x, y = self.root(node), self.root(neighborNode)
        if x == y: return
        # weighted quick-union
        if self.sz[x] > self.sz[y]:
            x, y = y, x
        # link smaller tree below larger tree
        self.id[x] = y
        self.sz[y] += self.sz[x]
        self.count -= 1
```

Time limit exceeded error. This solution is O(k*m*n), cause every time calling the bfs, need to scan all possible surroundings.

```Python
class Solution(object):
    def numIslands2(self, m, n, positions):
        """
        :type m: int
        :type n: int
        :type positions: List[List[int]]
        :rtype: List[int]
        """
        if m <= 0 or n <= 0 or not positions: return []
        res = [0] * len(positions)
        grid = [[0] * n for _ in xrange(m)]
        unique = 1

        for k in xrange(len(positions)):
            row, col = positions[k]
            if k == 0:
                res[k], grid[row][col] = 1, unique
            else:
                sameIsland = False
                for i, j in [(row-1, col), (row+1, col), (row, col-1), (row, col+1)]:
                    if 0 <= i < m and 0 <= j < n and grid[i][j] != 0:
                        sameIsland = True
                if not sameIsland:  # if no surrounding island
                    res[k] = res[k-1] + 1
                    grid[row][col] = unique
                else:
                    # when there is surrounding island
                    # do bfs to: count diff islands number, mark all the island with a unique value
                    countIsland = self.bfs(grid, unique, row, col, m, n)
                    res[k] = res[k-1] + 1 - countIsland
            unique += 1
        return res

    def bfs(self, grid, unique, row, col, m, n):
        visited = [[False] * n for _ in xrange(m)]
        queue = collections.deque([(row, col, [])])

        while queue:
            x, y, count = queue.popleft()
            grid[x][y], visited[x][y] = unique, True
            for i, j in [(x-1, y), (x+1, y), (x, y-1), (x, y+1)]:
                if 0 <= i < m and 0 <= j < n and grid[i][j] != 0 and not visited[i][j]:
                    if grid[i][j] not in count: count.append(grid[i][j])
                    visited[i][j], grid[i][j] = True, unique
                    queue.append((i, j, count))
        return len(count)
```
