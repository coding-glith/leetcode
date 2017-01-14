# Jump Game

> Given an array of non-negative integers, you are initially positioned at the first index of the array.

> Each element in the array represents your maximum jump length at that position.

> Determine if you are able to reach the last index.

> For example:

> A = [2,3,1,1,4], return true.

> A = [3,2,1,0,4], return false.

The idea here is to maintain an iterator index, and maxReach, as index will go from start to end one by one, if cannot reach to the end of array, index will be larger than maxReach starting from some point.

```Python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums) <= 1:
            return True
        index, maxReach = 0, 0
        while index < len(nums) and index <= maxReach:
            # index <= maxReach is a key to terminate the loop
            maxReach = max(index + nums[index], maxReach)
            index += 1
            if maxReach == len(nums)-1:
                return True
        return index == len(nums)
```

This DP solution is checking from end to start, but get 'time limit exceeded'. This is O(n^2) time complexity.

```Python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums) <= 1:
            return True
        result = [False for indx in xrange(len(nums))]
        result[len(nums)-1] = True
        for indx in xrange(len(nums)-2, -1, -1):
            for inner in xrange(indx+1, len(nums)):
                if nums[indx] >= (inner-indx) and result[inner] == True:
                    result[indx] = True
        return result[0]
```

# Jump Game II

> Given an array of non-negative integers, you are initially positioned at the first index of the array.

> Each element in the array represents your maximum jump length at that position.

> Your goal is to reach the last index in the minimum number of jumps.

> For example:

> Given array A = [2,3,1,1,4]

> The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

> Note:

> You can assume that you can always reach the last index.

This is still O(N) solution. For start index, check the maxReach from range(start, end+1), this ensures the maxReach to be the final value of this range, so after this check, we can increase result by 1.

```Python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        result, maxReach, start, end = 0, 0, 0, 0
        while maxReach < len(nums) - 1:
            for i in xrange(start, end+1):
                maxReach = max(maxReach, i + nums[i])
            start, end = end + 1, maxReach
            result += 1
        return result
```
