# Paint Fence

> There is a fence with n posts, each post can be painted with one of the k colors.

> You have to paint all the posts such that no more than two adjacent fence posts have the same color.

> Return the total number of ways you can paint the fence.

> Note:

> n and k are non-negative integers.

The idea is to calculate two cases separately: last two posts have same/different color. refer to leetcode [discussion](https://discuss.leetcode.com/topic/23426/o-n-time-java-solution-o-1-space)

```
1: k
   same              diff
2: k*1             + k*(k-1)
   diff              same              diff
3: k*1*(k-1)       + k*(k-1)*1       + k*(k-1)*(k-1)
   same              diff              diff              same              diff
4: k*1*(k-1)*1     + k*1*(k-1)*(k-1) + k*(k-1)*1*(k-1) + k*(k-1)*(k-1)*1 + k*(k-1)*(k-1)*(k-1)
   this same is correct because 4th have same color with 1st and 2nd.
```

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
        same, diff = k, k*(k-1)
        for i in xrange(2, n):
            diff, same = (same + diff) * (k-1), diff
        return diff + same
```
