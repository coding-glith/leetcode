# Water and Jug Problem

> You are given two jugs with capacities x and y litres. There is an infinite amount of water supply available. You need to determine whether it is possible to measure exactly z litres using these two jugs.

> If z liters of water is measurable, you must have z liters of water contained within one or both buckets by the end.

> Operations allowed:

> * Fill any of the jugs completely with water.

> * Empty any of the jugs.

> * Pour water from one jug into another till the other jug is completely full or the first jug itself is empty.

> Example 1: (From the famous "Die Hard" example)

> ```
Input: x = 3, y = 5, z = 4
Output: True
Example 2:
```

> ```
Input: x = 2, y = 6, z = 5
Output: False
```

From leetcode [discussion](https://discuss.leetcode.com/topic/49238/math-solution-java-solution/2). 

```
Bézout's identity (also called Bézout's lemma) is a theorem in the elementary theory of numbers:

let a and b be nonzero integers and let d be their greatest common divisor. Then there exist integers x
and y such that ax+by=d

In addition, the greatest common divisor d is the smallest positive integer that can be written as ax + by

every integer of the form ax + by is a multiple of the greatest common divisor d.
```

```Python
class Solution(object):
    def canMeasureWater(self, x, y, z):
        """
        :type x: int
        :type y: int
        :type z: int
        :rtype: bool
        """
        def GCD(x, y):
            for i in xrange(min(x, y), 0, -1):
                if x % i == 0 and y % i == 0:
                    return i
            return 1
        if x + y < z: return False
        if x == z or y == z or x+y == z: return True
        if 0 in [x, y]: return x+y == z
        return z % GCD(x, y) == 0
```
