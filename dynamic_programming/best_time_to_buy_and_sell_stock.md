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

The idea is to check for each index inside list of the maximum profit in the left and right, then the maximum sum would be the maximum profit for two transactions limit.

```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) <= 1:
            return 0
        
        # define two lists for maxProfit of left/right sublist of a specific index
        leftProfit = [0 for i in xrange(len(prices))]
        rightProfit = [0 for i in xrange(len(prices))]
        
        # calculate maxProfit for list from 0 to index
        minValue = prices[0]
        for indx in xrange(1, len(prices)):
            minValue = min(minValue, prices[indx])
            leftProfit[indx] = max(leftProfit[indx-1], prices[indx]-minValue)
        
        # calculate maxProfit for list from index to the end
        maxValue = prices[-1]
        for indx in xrange(len(prices)-2, -1, -1):
            maxValue = max(maxValue, prices[indx])
            rightProfit[indx] = max(rightProfit[indx+1], maxValue - prices[indx])
        
        # the result would be: max of leftProfit + rightProfit
        result = 0
        for indx in xrange(1, len(prices)):
            result = max(result, leftProfit[indx] + rightProfit[indx])
        
        return result
```

# Best Time to Buy and Sell Stock IV

> Say you have an array for which the ith element is the price of a given stock on day i.

> Design an algorithm to find the maximum profit. You may complete at most k transactions.

> Note:

> You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

Didn't fully understand yet :-(

```Python
class Solution(object):
    def maxProfit(self, k, prices):
        """
        :type k: int
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) <= 1:
            return 0
        if k >= len(prices) / 2:  # becomes unlimited number of transaction
            return self.maxProfitNoLimit(prices)

        dp = [None] * (2 * k + 1)
        dp[0] = 0
        for day in xrange(len(prices)):
            for transac in xrange(1, min(2*k, day+1)+1):
                dp[transac] = max(dp[transac], dp[transac-1]+prices[day]*[1,-1][transac%2])
        return dp[2*k]

    def maxProfitNoLimit(self, prices):
        maxProfit = 0
        for indx in xrange(1, len(prices)):
            maxProfit = max(maxProfit, maxProfit + prices[indx] - prices[indx - 1])
        return maxProfit
```
