# Guess Number Higher or Lower

> We are playing the Guess Game. The game is as follows:

> I pick a number from 1 to n. You have to guess which number I picked.

> Every time you guess wrong, I'll tell you whether the number is higher or lower.

> You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):

> ```
-1 : My number is lower
 1 : My number is higher
 0 : Congrats! You got it!
```
 
> Example:

> ```
n = 10, I pick 6.
Return 6.
```

```Python
# The guess API is already defined for you.
# @param num, your guess
# @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
# def guess(num):

class Solution(object):
    def guessNumber(self, n):
        """
        :type n: int
        :rtype: int
        """
        start, end = 1, n
        while start <= end:
            mid = start + (end - start) / 2
            if guess(mid) == -1:
                end = mid - 1
            elif guess(mid) == 1:
                start = mid + 1
            else:
                return mid
        return n
```

# Guess Number Higher or Lower II

> We are playing the Guess Game. The game is as follows:

> I pick a number from 1 to n. You have to guess which number I picked.

> Every time you guess wrong, I'll tell you whether the number I picked is higher or lower.

> However, when you guess a particular number x, and you guess wrong, you pay $x. You win the game when you guess the number I picked.

> Example:

> ```
n = 10, I pick 8.
First round:  You guess 5, I tell you that it's higher. You pay $5.
Second round: You guess 7, I tell you that it's higher. You pay $7.
Third round:  You guess 9, I tell you that it's lower. You pay $9.
Game over. 8 is the number I picked.
You end up paying $5 + $7 + $9 = $21.
```

> Given a particular n ≥ 1, find out how much money you need to have to guarantee a win.

> Hint:

> * The best strategy to play the game is to minimize the maximum loss you could possibly face. Another strategy is to minimize the expected loss. Here, we are interested in the first scenario.
> * Take a small example (n = 3). What do you end up paying in the worst case?

> * Check out this article if you're still stuck.

```Python
class Solution(object):
    def getMoneyAmount(self, n):
        """
        :type n: int
        :rtype: int
        """
        def dp(table, start, end):
            if start >= end:
                return 0
            if table[start][end] != 0:
                return table[start][end]
            res = float('inf')
            for i in xrange(start, end+1):
                tmp = i + max(dp(table, start, i-1), dp(table, i+1, end))
                res = min(res, tmp)
            table[start][end] = res
            return res
        table = [[0] * (n+1) for _ in xrange(n+1)]
        return dp(table, 1, n)
```
