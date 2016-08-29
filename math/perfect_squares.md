# Perfect Squares

> Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

> For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.

BFS solution here.

```Python
class Solution(object):
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        # list all available sqaure numbers
        squareNums = [i*i for i in xrange(1, int(math.sqrt(n))+1)]
        level = 0
        cur = [0]
        while True:
            nextLevel = []
            for i in cur:
                for s in squareNums:
                    if i + s == n:
                        return level + 1
                    if i + s < n:
                        nextLevel.append(i + s)
            cur = list(set(nextLevel))
            level += 1
        return level
```
