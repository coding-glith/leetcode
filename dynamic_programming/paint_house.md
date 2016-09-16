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

# Paint House II

> There are a row of n houses, each house can be painted with one of the k colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

> The cost of painting each house with a certain color is represented by a n x k cost matrix. For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses.

> Note:

> All costs are positive integers.

> Follow up:

> Could you solve it in O(nk) runtime?

Below is a better idea, but don't understand the settings for min1, and min2.

```Python
class Solution(object):
    def minCostII(self, costs):
        """
        :type costs: List[List[int]]
        :rtype: int
        """
        if not costs or len(costs) == 0:
            return 0
        n, k = len(costs), len(costs[0])
        min1, min2 = -1, -1
        for i in xrange(n):
            last1, last2 = min1, min2
            min1, min2 = -1, -1   # don't understand this part
            for j in xrange(k):
                # costs[i][j] means house i with color j
                if j == last1:   # if color is the same as last one
                    # choose last2
                    costs[i][j] += costs[i-1][last2] if last2 >= 0 else 0
                else:
                    costs[i][j] += costs[i-1][last1] if last1 >= 0 else 0
                if min1 < 0 or costs[i][j] < costs[i][min1]:
                    min1, min2 = j, min1
                elif min2 < 0 or costs[i][j] < costs[i][min2]:
                    min2 = j
        return costs[-1][min1]
```

Exact same idea but O(n*k^2) runtime.

```Python
class Solution(object):
    def minCostII(self, costs):
        """
        :type costs: List[List[int]]
        :rtype: int
        """
        if len(costs) == 0:
            return 0
        last = list(costs[0])
        for i in xrange(1, len(costs)):
            cur = [0] * len(costs[0])
            for k in xrange(len(cur)):
                tmp = list(last)
                tmp.pop(k)
                cur[k] = min(tmp) + costs[i][k]
            last = list(cur)
        return min(last)
```
