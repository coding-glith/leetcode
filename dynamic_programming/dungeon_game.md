# Dungeon Game

> The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

> The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

> Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).

> In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

> Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

> For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path RIGHT-> RIGHT -> DOWN -> DOWN.

> ```
-2(K)  -3    3
-5     -10   1
10     30    -5(P)
```

> Notes:

> * The knight's health has no upper bound.

> * Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.

The idea of this solution is to track back from the pricess position. Since we have to maintain 1 hp at each column, we need to get max(1, dp). Check further explanation from leetcode [discussion](https://discuss.leetcode.com/topic/7633/best-solution-i-have-found-with-explanations)

```Python
class Solution(object):
    def calculateMinimumHP(self, dungeon):
        """
        :type dungeon: List[List[int]]
        :rtype: int
        """
        if not dungeon or len(dungeon[0]) == 0:
            return 0
        row, col = len(dungeon), len(dungeon[0])
        dp = [[0] * col for _ in xrange(row)]
        for r in xrange(row-1, -1, -1):
            for c in xrange(col-1, -1, -1):
                if r == row - 1 and c == col - 1:
                    dp[r][c] = max(1, 1 - dungeon[r][c])
                elif r == row - 1:
                    dp[r][c] = max(1, dp[r][c+1] - dungeon[r][c])
                elif c == col - 1:
                    dp[r][c] = max(1, dp[r+1][c] - dungeon[r][c])
                else:
                    dp[r][c] = max(1, min(dp[r+1][c], dp[r][c+1]) - dungeon[r][c])
        return dp[0][0]
```
