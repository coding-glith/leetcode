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

Sort the array and check if sub in list.

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
        res = []
        self.getCombine(res, [], 1, k, n)
        return res

    def getCombine(self, res, sub, idx, k, target):
        if len(sub) == k and target == 0:
            res.append(list(sub))
            return
        for i in xrange(idx, 10):
            if target - i >= 0:
                sub.append(i)
                self.getCombine(res, sub, i+1, k, target - i)
                sub.pop()
```

# Combination Sum IV

> Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

> Example:

> ```
nums = [1, 2, 3]
target = 4
The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
Note that different sequences are counted as different combinations.
Therefore the output is 7.
```

> Follow up:

> * What if negative numbers are allowed in the given array?

> * How does it change the problem?

> * What limitation we need to add to the question to allow negative numbers?

If negative numbers are allowed, then need to limit the number of times a value can be used in the array, otherwise it will be infinite number of results.

DP solution. The index in res is the goal in every round. Then check the values in nums, if larger, break of course because of we've sorted the array. if equal, then this value itself becomes a result, if smaller, then need to combine with other results, that is current goal - current value.

```Python
class Solution(object):
    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if not nums: return 0
        nums.sort()
        res = [0] * (target + 1)
        for goal in xrange(1, len(res)):
            for val in nums:
                if val > goal: break
                elif val == goal: res[goal] += 1
                else: res[goal] += res[goal - val]
        return res[target]
```

Use backtracking to get all possible combinations and return the length of the results. But this requires extra steps, we don't need all the combinations.

```Python
class Solution(object):
    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if not nums: return 0
        res = []
        self.getCombine(res, [], nums, target)
        return len(res)

    def getCombine(self, res, sub, nums, target):
        if target == 0:
            res.append(list(sub))
            return
        for val in nums:
            if target - val >= 0:
                sub.append(val)
                self.getCombine(res, sub, nums, target - val)
                sub.pop()
```
