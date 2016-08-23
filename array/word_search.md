# Word Search

> Given a 2D board and a word, find if the word exists in the grid.

> The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

> For example,

> Given board =

> ```
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```

> word = "ABCCED", -> returns true,

> word = "SEE", -> returns true,

> word = "ABCB", -> returns false.

```Python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        # for every element in the board, check for word once
        for row in xrange(len(board)):
            for col in xrange(len(board[0])):
                if self.helper(row, col, board, word, 0):
                    return True
        return False

    def helper(self, row, col, board, word, idx):
        if idx == len(word):
            return True
        if row < 0 or row >= len(board) or col < 0 or col >= len(board[row]):
            return False
        if board[row][col] != word[idx]:
            return False
        board[row][col] = '*'  # the trick here is to mark checked location
        res = self.helper(row + 1, col, board, word, idx + 1) \
              or self.helper(row - 1, col, board, word, idx + 1) \
              or self.helper(row, col + 1, board, word, idx + 1) \
              or self.helper(row, col - 1, board, word, idx + 1)
        board[row][col] = word[idx]
        return res
```
