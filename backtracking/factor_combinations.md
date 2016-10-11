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
        if n <= 1: return []
        return self.getFact(n, 2, [], [])

    def getFact(self, target, val, sub, res):
        while val * val <= target:   # only check the firsrt half part
            if target % val == 0:  # if can divide
                res.append(list(sub + [val, target / val]))   # to accompany val * val <= target
                # currently sub didn't change
                self.getFact(target / val, val, sub + [val], res)   # already checked variable "val"
            val += 1
        return res
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
