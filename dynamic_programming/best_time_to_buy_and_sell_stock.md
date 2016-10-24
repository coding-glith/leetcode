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

The idea is to maintain two array left and right, left keeps the max profit from left to the index, right keeps the max profit from index to right. Then go through the two array to find out the max two transactions.

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

From leetcode [discussion](https://discuss.leetcode.com/topic/26169/clean-java-dp-solution-with-comment):

```
/**
 * dp[i, j] represents the max profit up until prices[j] using at most i transactions. 
 * dp[i, j] = max(dp[i, j-1], prices[j] - prices[jj] + dp[i-1, jj]) { jj in range of [0, j-1] }
 *          = max(dp[i, j-1], prices[j] + max(dp[i-1, jj] - prices[jj]))
 * dp[0, j] = 0; 0 transactions makes 0 profit
 * dp[i, 0] = 0; if there is only one price data point you can't make any transaction.
 */
 ```

```Python
class Solution(object):
    def maxProfit(self, k, prices):
        """
        :type k: int
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) <= 1: return 0

        def maxTrans(prices):
            res = 0
            for i in xrange(1, len(prices)):
                res = max(res, res + prices[i] - prices[i-1])
            return res
        if k >= len(prices) / 2:
            return maxTrans(prices)

        dp = [[0 for j in xrange(len(prices))] for i in xrange(k+1)]
        for num in xrange(1, k+1):
            localMax = dp[num-1][0] - prices[0]
            for day in xrange(1, len(prices)):
                dp[num][day] = max(dp[num][day-1], prices[day] + localMax)
                localMax = max(localMax, dp[num-1][day] - prices[day])
        return dp[k][-1]
```

# Best Time to Buy and Sell Stock with Cooldown

> Say you have an array for which the ith element is the price of a given stock on day i.

> Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

> * You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

> * After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

> Example:

> ```
prices = [1, 2, 3, 0, 2]
maxProfit = 3
transactions = [buy, sell, cooldown, buy, sell]
```

State transition method from leetcode [discussion](https://discuss.leetcode.com/topic/30680/share-my-dp-solution-by-state-machine-thinking)

```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) <= 1: return 0
        rest, buy, sell = 0, -prices[0], 0   # for sell in index 0
        for price in prices:
            prev_sell = sell
            sell = buy + price   # transit from buy
            buy = max(buy, rest - price)   # stay at buy or transit from rest
            rest = max(rest, prev_sell)    # stay at rest or transit from buy
        return max(rest, sell)
```
