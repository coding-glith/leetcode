# Flip Game

> You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

> Write a function to compute all possible states of the string after one valid move.

> For example, given s = "++++", after one move, it may become one of the following states:

> ```
[
  "--++",
  "+--+",
  "++--"
]
```

> If there is no valid move, return an empty list [].

```Python
class Solution(object):
    def generatePossibleNextMoves(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        if len(s) <= 1:
            return []
        result = []
        for i in xrange(len(s)-1):
            if s[i] == '+' and s[i+1] == '+':
                result.append(s[0:i]+'--'+s[i+2:])
        return result
```

# Flip Game II

> You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

> Write a function to determine if the starting player can guarantee a win.

> For example, given s = "++++", return true. The starting player can guarantee a win by flipping the middle "++" to become "+--+".

> Follow up:

> * Derive your algorithm's runtime complexity.

Using memorization to store the status of substring, so previous results can be reused to save time. Check leetcode [discussion](https://discuss.leetcode.com/topic/27291/memoization-3150ms-130ms-44ms-python).

```Python
class Solution(object):
    def canWin(self, s):
        """
        :type s: str
        :rtype: bool
        """
        memo = {}
        
        def can(s):
            if s not in memo:
                memo[s] = any(s[i:i+2] == "++" and not can(s[:i]+"-"+s[i+2:]) for i in xrange(len(s)))
            return memo[s]
        
        return can(s)
```
