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

# Valid Perfect Square

> Given a positive integer num, write a function which returns True if num is a perfect square else False.

> Note: Do not use any built-in library function such as sqrt.

> Example 1:

> ```
Input: 16
Returns: True
```

> Example 2:

> ```
Input: 14
Returns: False
```

```Python
class Solution(object):
    def isPerfectSquare(self, num):
        """
        :type num: int
        :rtype: bool
        """
        if num == 1:
            return True
        start, end = 1, num/2+1
        while start <= end:
            mid = start + (end - start) / 2
            if mid * mid == num:
                return True
            elif mid * mid > num:
                end = mid - 1
            else:
                start = mid + 1
        return False
```
