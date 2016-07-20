# Climbing Stairs

> You are climbing a stair case. It takes n steps to reach to the top.

> Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

```Python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 1:
            return n
        # think of n as the total number of steps
        numWays = [0 for indx in range(n)]
        numWays[0] = 1
        numWays[1] = 2
        for indx in range(2, n):
            numWays[indx] = numWays[indx-1] + numWays[indx-2]
        return numWays[n-1]
```
