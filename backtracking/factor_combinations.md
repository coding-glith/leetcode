# Factor Combinations

> Numbers can be regarded as product of its factors. For example,

> ```
8 = 2 x 2 x 2;
  = 2 x 4.
```

> Write a function that takes an integer n and return all possible combinations of its factors.

> Note: 

> * You may assume that n is always positive.

> * Factors should be greater than 1 and less than n.

> Examples: 

> input: 1; output: []

> input: 37; output: []

> input: 12; output:

> ```
[
  [2, 6],
  [2, 2, 3],
  [3, 4]
]
```

> input: 32; output:

> ```
[
  [2, 16],
  [2, 2, 8],
  [2, 2, 2, 4],
  [2, 2, 2, 2, 2],
  [2, 4, 4],
  [4, 8]
]
```

Recursive solution.

```Python
class Solution(object):
    def getFactors(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        if n <= 1:
            return []
        def factor(n, elem, resList, result):
            while elem * elem <= n:  # no need to consider value > n/2
                if n % elem == 0:
                    result.append(list(resList+[elem, n/elem]))
                    factor(n/elem, elem, resList+[elem], result)
                elem += 1
            return result
        return factor(n, 2, [], [])
```

The following code is "Memory Limit Exceeded" for input = 23848713. :-(

```Python
class Solution(object):
    def getFactors(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        if n <= 1:
            return []
        result = []
        self.factor(result, [], n, 2, n)
        return result

    def factor(self, result, elems, n, start, remain):
        if remain <= 1:
            result.append(list(elems))
            return
        for val in range(start, n):
            if remain % val == 0:
                elems.append(val)
                self.factor(result, elems, n, val, remain/val)
                elems.pop()
```
