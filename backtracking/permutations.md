# Permutations

> Given a collection of distinct numbers, return all possible permutations.

> For example,

> [1,2,3] have the following permutations:

> ```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```Python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return [[]]
        result = []
        self.permuteList(result, [], nums)
        return result

    def permuteList(self, result, subList, nums):
        if len(subList) == len(nums):
            result.append(list(subList))
            return
        for indx in xrange(len(nums)):
            if nums[indx] not in subList:
                subList.append(nums[indx])
                self.permuteList(result, subList, nums)
                subList.pop()
```

# Permutations II

> Given a collection of numbers that might contain duplicates, return all possible unique permutations.

> For example,

> [1,1,2] have the following unique permutations:

> ```
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

```Python

```
