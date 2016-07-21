# Combinations

> Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

> For example,

> If n = 4 and k = 2, a solution is:

> ```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

This idea takes advantage that result values is getting from 1 to n.

```Python
class Solution(object):
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        if k > n or k <=0 or n <= 0:
            return [[]]
        result = []
        indx = 0  # iterator for the subList
        subList = [0 for val in range(k)]
        while indx >= 0:
            subList[indx] += 1   # take advantage of value from 1 to n
            if subList[indx] > n:
                indx -= 1
            elif indx == k - 1:
                result.append(list(subList))
            else:
                indx += 1
                subList[indx] = subList[indx - 1]
        return result
```

The following backtracking method is 'run time exceeds'. :-(

```Python
class Solution(object):
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        if k > n or k <=0 or n <= 0:
            return [[]]
        result = []
        self.combinationList(result, [], 1, n, k)
        return result

    def combinationList(self, result, subList, start, num, k):
        if len(subList) == k:
            # should have keyword 'list' below because otherwise it's passing reference
            result.append(list(subList))
            return
        for indx in range(start, num+1):
            subList.append(indx)
            self.combinationList(result, subList, indx+1, num, k)
            subList.pop()
```
