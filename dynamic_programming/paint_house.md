# Paint House

> There are a row of n houses, each house can be painted with one of the three colors: red, blue or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

> The cost of painting each house with a certain color is represented by a n x 3 cost matrix. For example, costs[0][0] is the cost of painting house 0 with color red; costs[1][2] is the cost of painting house 1 with color green, and so on... Find the minimum cost to paint all houses.

> Note:

> All costs are positive integers.

```Python
class Solution(object):
    def minCost(self, costs):
        """
        :type costs: List[List[int]]
        :rtype: int
        """
        if len(costs) == 0:
            return 0
        lastR, lastB, lastG = costs[0]
        for i in xrange(1, len(costs)):
            curR = min(lastB, lastG) + costs[i][0]
            curB = min(lastR, lastG) + costs[i][1]
            curG = min(lastR, lastB) + costs[i][2]
            lastR, lastB, lastG = curR, curB, curG
        return min(lastR, lastB, lastG) 
```
