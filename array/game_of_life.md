# Game of Life

> According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

> Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

> * Any live cell with fewer than two live neighbors dies, as if caused by under-population.

> * Any live cell with two or three live neighbors lives on to the next generation.

> * Any live cell with more than three live neighbors dies, as if by over-population..

> * Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

> Write a function to compute the next state (after one update) of the board given its current state.

> Follow up: 

> * Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.

> * In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

```Python
class Solution(object):
    def gameOfLife(self, board):
        """
        :type board: List[List[int]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        if not board or len(board) == 0 or len(board[0]) == 0:
            return
        for row in xrange(0, len(board)):
            for col in xrange(0, len(board[0])):
                sumVal = self.checkEightNeighborsSum(row, col, board)
                if (board[row][col] == 1 and (sumVal in [2, 3])) or (board[row][col] == 0 and sumVal == 3):
                    board[row][col] |= 0x02 # use the second bit to store results
        for row in xrange(0, len(board)):
            for col in xrange(0, len(board[0])):
                board[row][col] >>= 1   # return only the second bits

    def checkEightNeighborsSum(self, row, col, board):
        sumVal = 0
        for i in xrange(row - 1, row + 2):
            for j in xrange(col -1, col + 2):
                if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]):
                    continue
                if board[i][j] & 0x01 == 1:  # just check the first bit
                    sumVal += 1
        return sumVal - board[row][col]
```
