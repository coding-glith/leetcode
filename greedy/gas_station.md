# Gas Station

> There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

> You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

> Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

> Note:

> The solution is guaranteed to be unique.

"remain" and "total" represent the local and global optimum for this greedy algorithm.

```Python
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        if len(gas) == 0:
            return -1
        result = 0
        remain, total = 0, 0
        for indx in range(len(gas)):
            remain += gas[indx] - cost[indx]
            if remain < 0:
                result = indx + 1 # make sure the remaining at this point is larger than 0
                remain = 0
            total += gas[indx] - cost[indx]
            # total is the total remaining for N stations
        if total < 0:
            return -1
        else:
            return result
```
