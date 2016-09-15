# Climbing Stairs

> You are climbing a stair case. It takes n steps to reach to the top.

> Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

This solution is space efficient than the other one. The idea is the same, at current step, you can either reach from previous step by one more step or from previous of previous step by two steps. Therefore, the number of ways to reach to current step is the sum of the two cases.

```Python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 2:
            return n
        # need to know the number of ways for:
        # previous step and previous of previous step
        numWays2Prev = 1
        numWaysPrev = 2
        for indx in range(3, n+1):
            tmp = numWays2Prev + numWaysPrev  # 2Prev should reach directly to cur, otherwise it's Prev
            numWays2Prev, numWaysPrev = numWaysPrev, tmp
        return numWaysPrev
```

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
