# Integer Break

> Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

> For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).

> Note: You may assume that n is not less than 2 and not larger than 58.

> Hint:

> * There is a simple O(n) solution to this problem.

> * You may check the breaking results of n ranging from 7 to 10 to discover the regularities.

```Python
class Solution(object):
    def integerBreak(self, n):
        """
        :type n: int
        :rtype: int
        """
        dp = [0] * (n+1)
        dp[2] = 1
        for i in xrange(3, n+1):
            for j in xrange(1, i-1):
                dp[i] = max(dp[i], j*max(i-j, dp[i-j]))
        return dp[-1]
```
