# Candy

> There are N children standing in a line. Each child is assigned a rating value.

> You are giving candies to these children subjected to the following requirements:

> * Each child must have at least one candy.

> * Children with a higher rating get more candies than their neighbors.

> What is the minimum candies you must give?

The idea is to go from left to right and right to left. But the second round should take care of any duplicate add on cases.

```Python
class Solution(object):
    def candy(self, ratings):
        """
        :type ratings: List[int]
        :rtype: int
        """
        if len(ratings) == 0:
            return 0
        result = [1 for indx in xrange(len(ratings))]
        for indx in xrange(1, len(ratings)):
            if ratings[indx] > ratings[indx - 1]:
                result[indx] = result[indx-1] + 1
        for indx in xrange(len(ratings)-2, -1, -1):
            if ratings[indx] > ratings[indx+1] and result[indx] <= result[indx+1]:
                result[indx] = result[indx+1] + 1
        return sum(result)  
```
