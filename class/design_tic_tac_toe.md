# Design Tic-Tac-Toe

> Design a Tic-tac-toe game that is played between two players on a n x n grid.

> You may assume the following rules:

> * A move is guaranteed to be valid and is placed on an empty block.

> * Once a winning condition is reached, no more moves is allowed.

> * A player who succeeds in placing n of their marks in a horizontal, vertical, or diagonal row wins the game.

> Example:

> ```
Given n = 3, assume that player 1 is "X" and player 2 is "O" in the board.
TicTacToe toe = new TicTacToe(3);
toe.move(0, 0, 1); -> Returns 0 (no one wins)
|X| | |
| | | |    // Player 1 makes a move at (0, 0).
| | | |
toe.move(0, 2, 2); -> Returns 0 (no one wins)
|X| |O|
| | | |    // Player 2 makes a move at (0, 2).
| | | |
toe.move(2, 2, 1); -> Returns 0 (no one wins)
|X| |O|
| | | |    // Player 1 makes a move at (2, 2).
| | |X|
toe.move(1, 1, 2); -> Returns 0 (no one wins)
|X| |O|
| |O| |    // Player 2 makes a move at (1, 1).
| | |X|
toe.move(2, 0, 1); -> Returns 0 (no one wins)
|X| |O|
| |O| |    // Player 1 makes a move at (2, 0).
|X| |X|
toe.move(1, 0, 2); -> Returns 0 (no one wins)
|X| |O|
|O|O| |    // Player 2 makes a move at (1, 0).
|X| |X|
toe.move(2, 1, 1); -> Returns 1 (player 1 wins)
|X| |O|
|O|O| |    // Player 1 makes a move at (2, 1).
|X|X|X|
```

> Follow up:

> Could you do better than O(n2) per move() operation?

> Hint:

> * Could you trade extra space such that move() operation can be done in O(1)?

> * You need two arrays: int rows[n], int cols[n], plus two variables: diagonal, anti_diagonal.

```Python
class TicTacToe(object):

    def __init__(self, n):
        """
        Initialize your data structure here.
        :type n: int
        """
        self.rowArray = [0] * n
        self.colArray = [0] * n
        self.diagonal = 0
        self.antidia = 0
        self.N = n
        

    def move(self, row, col, player):
        """
        Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins.
        :type row: int
        :type col: int
        :type player: int
        :rtype: int
        """
        if player == 1:
            self.rowArray[row] += 1
            self.colArray[col] += 1
            if row == col: self.diagonal += 1
            if row + col == self.N - 1: self.antidia += 1
        else:
            self.rowArray[row] -= 1
            self.colArray[col] -= 1
            if row == col: self.diagonal -= 1
            if row + col == self.N - 1: self.antidia -= 1
        if self.N in [self.rowArray[row], self.colArray[col], self.diagonal, self.antidia]:
            return 1
        elif -self.N in [self.rowArray[row], self.colArray[col], self.diagonal, self.antidia]:
            return 2
        else: return 0
        


# Your TicTacToe object will be instantiated and called as such:
# obj = TicTacToe(n)
# param_1 = obj.move(row,col,player)
```
