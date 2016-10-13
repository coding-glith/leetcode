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
        # for each elem in board, check for word as a start point
        for row in xrange(len(board)):
            for col in xrange(len(board[0])):
                if self.check(row, col, 0, board, word):
                    return True
        return False

    def check(self, row, col, idx, board, word):
        if idx == len(word): return True    # finish the last character in word
        if row < 0 or row >= len(board) or col < 0 or col >= len(board[0]): return False
        if board[row][col] != word[idx]: return False
        board[row][col] = '*'   # mark the checked location as *
        res = self.check(row-1, col, idx+1, board, word) or \
              self.check(row+1, col, idx+1, board, word) or \
              self.check(row, col-1, idx+1, board, word) or \
              self.check(row, col+1, idx+1, board, word)
        board[row][col] = word[idx]   # reset board value back from * to original value
        return res
```

# Word Search II

> Given a 2D board and a list of words from the dictionary, find all words in the board.

> Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

> For example,

> Given words = ["oath","pea","eat","rain"] and board =

> ```
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
```

> Return ["eat","oath"].

> Note:

> You may assume that all inputs are consist of lowercase letters a-z.

> hint:

> You would need to optimize your backtracking to pass the larger test. Could you stop backtracking earlier?

> If the current candidate does not exist in all words' prefix, you could stop backtracking immediately. What kind of data structure could answer such query efficiently? Does a hash table work? Why or why not? How about a Trie? If you would like to learn how to implement a basic trie, please work on this problem: Implement Trie (Prefix Tree) first.

```Python

```
