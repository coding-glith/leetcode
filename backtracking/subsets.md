# Subsets

> Given a set of distinct integers, nums, return all possible subsets.

> Note: The solution set must not contain duplicate subsets.

> For example,

> If nums = [1,2,3], a solution is:

> ```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

```Python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return [[]]
        result = []
        self.subset(result, [], 0, nums)
        return result

    def subset(self, result, subList, start, nums):
        if subList not in result:
            result.append(list(subList))
        for indx in xrange(start, len(nums)):
            subList.append(nums[indx])
            self.subset(result, subList, indx + 1, nums)
            subList.pop()
```

# Subsets II

> Given a collection of integers that might contain duplicates, nums, return all possible subsets.

> Note: The solution set must not contain duplicate subsets.

> For example,

> If nums = [1,2,2], a solution is:

> ```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

```Python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return [[]]
        result = []
        nums.sort()  # make sure check no duplicates works
        self.subset(result, [], 0, nums)
        return result

    def subset(self, result, subList, start, nums):
        if subList not in result:
            result.append(list(subList))
        for indx in xrange(start, len(nums)):
            subList.append(nums[indx])
            self.subset(result, subList, indx + 1, nums)
            subList.pop()
```
