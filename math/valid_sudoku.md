# Valid Sudoku

> Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

> The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

> ![alt text](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png "A partially filled sudoku which is valid.")

> Note:

> A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

```Python
class Solution(object):
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        # check rows
        for elem in board:
            if not self.isValid(list(elem)):
                return False
        # check columns
        for col in xrange(len(board[0])):
            tmp = []
            for row in xrange(len(board)):
                tmp.append(board[row][col])
            if not self.isValid(tmp):
                return False
        # check 3 * 3 board
        for col in xrange(0, len(board[0]), 3):
            tmp = []
            for row in xrange(0, len(board), 3):
                tmp.append(board[row][col:col+3]+board[row+1][col:col+3]+board[row+2][col:col+3])
                if not self.isValid(list(tmp[0])):
                    return False
                tmp = []
        return True
        
    def isValid(self, l):
        for elem in l:
            if elem != '.' and l.count(elem) > 1:
                return False
        return True
```
