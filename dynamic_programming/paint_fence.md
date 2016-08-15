# Paint Fence

> There is a fence with n posts, each post can be painted with one of the k colors.

> You have to paint all the posts such that no more than two adjacent fence posts have the same color.

> Return the total number of ways you can paint the fence.

> Note:

> n and k are non-negative integers.

The idea is to calculate two cases separately: last two posts have same/different color.

```Python
class Solution(object):
    def numWays(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: int
        """
        if n == 0:
            return 0
        if n == 1:
            return k
        diffColorCounts = k*(k-1) # last two have different color
        sameColorCounts = k # last two have same color
        for i in xrange(2,n):
            tmp = diffColorCounts
            diffColorCounts = (diffColorCounts + sameColorCounts) * (k-1)
            sameColorCounts = tmp
        return diffColorCounts + sameColorCounts
```
