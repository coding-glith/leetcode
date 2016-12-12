# Jump Game

> Given an array of non-negative integers, you are initially positioned at the first index of the array.

> Each element in the array represents your maximum jump length at that position.

> Determine if you are able to reach the last index.

> For example:

> ```
A = [2,3,1,1,4], return true.
A = [3,2,1,0,4], return false.
```

```Python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        goal = len(nums) - 1
        for i in xrange(len(nums)-1, -1, -1):
            if i + nums[i] >= goal:
                goal = i
        return goal == 0
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

```Python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        res, lastIdx, nextIdx = 0, 0, 0
        while nextIdx < len(nums) - 1:
            res += 1
            lastIdx, nextIdx = nextIdx, max(i+nums[i] for i in xrange(lastIdx, nextIdx+1))
        return res
```
