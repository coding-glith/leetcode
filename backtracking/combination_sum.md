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

Maintain a start to make sure that there's no duplicate in the results.

```Python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        if not candidates: return [[]]
        res = []
        self.getCombine(res, [], 0, candidates, target)
        return res
    
    def getCombine(self, res, sub, start, nums, target):
        if target == 0:
            res.append(list(sub))
            return
        for i in xrange(start, len(nums)):
            if target - nums[i] >= 0:
                sub.append(nums[i])
                self.getCombine(res, sub, i, nums, target - nums[i])
                sub.pop()
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
class Solution(object):
    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        if len(candidates) == 0:
            return [[]]
        result = []
        candidates.sort()
        self.combineSum(result, [], 0, candidates, target)
        return result
    
    def combineSum(self, result, subList, start, candidates, target):
        if target == 0:
            if subList not in result:
                result.append(list(subList))
            return
        for indx in range(start, len(candidates)):
            if target > 0 and candidates[indx] <= target:
                subList.append(candidates[indx])
                self.combineSum(result, subList, indx + 1, candidates, target - candidates[indx])
                subList.pop()
```

# Combination Sum III

> Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

> Example 1:

> Input: k = 3, n = 7

> Output: [[1,2,4]]

> Example 2:

> Input: k = 3, n = 9

> Output: [[1,2,6], [1,3,5], [2,3,4]]

```Python
class Solution(object):
    def combinationSum3(self, k, n):
        """
        :type k: int
        :type n: int
        :rtype: List[List[int]]
        """
        if k <= 0 or n <= 0:
            return [[]]
        result = []
        self.combineSum(result, [], 1, k, n)
        return result

    def combineSum(self, result, subList, start, k, n):
        if n == 0 and len(subList) == k and subList not in result:
            result.append(list(subList))
            return
        for num in range(start, 10):
            if num <= n:
                subList.append(num)
                self.combineSum(result, subList, num+1, k, n - num)
                subList.pop()
```
