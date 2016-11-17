# Surrounded Regions

> Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

> A region is captured by flipping all 'O's into 'X's in that surrounded region.

> For example,

> ```
X X X X
X O O X
X X O X
X O X X
```
> After running your function, the board should be:

> ```
X X X X
X X X X
X X X X
X O X X
```

The idea is to go through the boarder of the board, if meet an 'O', mark all connected 'O' with 'S', then mark all left 'O' with 'X'. And finally revert 'S' back to 'O'.

```Python
class Solution(object):
    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        if not board or not board[0]: return
        for i in xrange(len(board)):
            for j in xrange(len(board[i])):
                if (i in (0, len(board)-1) or j in (0, len(board[0])-1)) and board[i][j] == 'O':
                    self.bfs(board, i, j)
        for i in xrange(len(board)):
            for j in xrange(len(board[i])):
                if board[i][j] == 'O':
                    board[i][j] = 'X'
        for i in xrange(len(board)):
            for j in xrange(len(board[i])):
                if board[i][j] == 'S':
                    board[i][j] = 'O'

    def bfs(self, board, i, j):
        visited = [[False] * len(board[0]) for _ in xrange(len(board))]
        visited[i][j] = True
        board[i][j] = 'S'
        queue = collections.deque([(i, j)])

        while queue:
            x, y = queue.popleft()
            for row, col in (x-1,y), (x+1,y), (x,y-1), (x,y+1):
                if 0 <= row < len(board) and 0 <= col < len(board[0]) and \
                   board[row][col] == 'O' and not visited[row][col]:
                    visited[row][col] = True
                    board[row][col] = 'S'
                    queue.append((row, col))
```
