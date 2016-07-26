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

The key idea is how to eleminate duplicate permutations. We maintain a visitFlag and check constantly to see if we are checking a duplicate value at the start level.

```Python
class Solution(object):
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 0:
            return [[]]
        result = []
        visitFlag = [0 for indx in range(len(nums))]
        nums.sort()
        self.permute(result, [], visitFlag, nums)
        return result

    def permute(self, result, subList, visitFlag, nums):
        if len(subList) == len(nums):
            result.append(list(subList))
            return
        for indx in xrange(len(nums)):
            if visitFlag[indx] == 1 or (indx != 0 and nums[indx] == nums[indx-1] and visitFlag[indx-1] == 0):
                continue
            subList.append(nums[indx])
            visitFlag[indx] = 1
            self.permute(result, subList, visitFlag, nums)
            subList.pop()
            visitFlag[indx] = 0
```
