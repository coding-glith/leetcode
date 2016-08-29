# Bulb Switcher

> There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the ith round, you toggle every i bulb. For the nth round, you only toggle the last bulb. Find how many bulbs are on after n rounds.

> Example:

> Given n = 3. 

> ```
At first, the three bulbs are [off, off, off].
After first round, the three bulbs are [on, on, on].
After second round, the three bulbs are [on, off, on].
After third round, the three bulbs are [on, off, off]. 
So you should return 1, because there is only one bulb is on.
```

Consider a light k will be turn triggered twice if sqrt(k) is a integer.

```Python
class Solution(object):
    def bulbSwitch(self, n):
        """
        :type n: int
        :rtype: int
        """
        return int(math.sqrt(n))
```

This intuitive idea gets time limit exceeded.

```Python
class Solution(object):
    def bulbSwitch(self, n):
        """
        :type n: int
        :rtype: int
        """
        res = [1] * n
        for i in xrange(2, 1+n):
            for j in xrange(n):
                if (j+1) % i == 0:
                    res[j] = 1 - res[j]
        return sum(res)
```
