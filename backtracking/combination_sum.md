# Combination Sum

> Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

> The same repeated number may be chosen from C unlimited number of times.

> Note:

> * All numbers (including target) will be positive integers.

> * The solution set must not contain duplicate combinations.

> For example, given candidate set [2, 3, 6, 7] and target 7, 

> A solution set is: 

> ```
[
  [7],
  [2, 2, 3]
]
```

```Python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        if len(candidates) == 0:
            return [[]]
        results = []
        self.combineSum(results, [], 0, candidates, target)
        return results

    def combineSum(self, results, subList, start, candidates, target):
        if target == 0:
            results.append(list(subList))
            return
        for indx in range(start, len(candidates)):
            if target > 0 and candidates[indx] <= target:
                subList.append(candidates[indx])
                self.combineSum(results, subList, indx, candidates, target-candidates[indx])
                subList.pop()
```

# Combination Sum II

> Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

> Each number in C may only be used once in the combination.

> Note:

> * All numbers (including target) will be positive integers.

> * The solution set must not contain duplicate combinations.

> For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8, 

> A solution set is: 

> ```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

```Python

```
