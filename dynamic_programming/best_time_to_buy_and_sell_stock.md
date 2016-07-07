# Best Time to Buy and Sell Stock

> Say you have an array for which the ith element is the price of a given stock on day i.

> If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

> Example 1:

> ```
Input: [7, 1, 5, 3, 6, 4]
Output: 5
max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

> Example 2:

> ```
Input: [7, 6, 4, 3, 1]
Output: 0
In this case, no transaction is done, i.e. max profit = 0.
```

```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) <= 1:
            return 0
        profit = 0
        prevMin = prices[0]
        for indx in xrange(1, len(prices)):
            profit = max(profit, prices[indx] - prevMin)
            if prices[indx] < prevMin:
                prevMin = prices[indx]
        return profit
```

# Best Time to Buy and Sell Stock II

> Say you have an array for which the ith element is the price of a given stock on day i.

> Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) <= 1:
            return 0
        profit = 0
        for indx in xrange(1, len(prices)):
            diff = prices[indx] - prices[indx-1]
            if diff > 0:
                profit += diff
        return profit
```

# Best Time to Buy and Sell Stock III

> Say you have an array for which the ith element is the price of a given stock on day i.

> Design an algorithm to find the maximum profit. You may complete at most two transactions.

> Note:

> You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

```Python

```
