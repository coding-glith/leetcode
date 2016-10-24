# Maximum Subarray

> Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

> For example, given the array [−2,1,−3,4,−1,2,1,−5,4],

> he contiguous subarray [4,−1,2,1] has the largest sum = 6.

> More practice:

> If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

The idea here is that maxSub[indx] is the maximum sum from 0 to indx, and the value of indx should always be included. global max is updated with local value.

```Python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums: return 0
        maxSub, res = [0] * len(nums), nums[0]
        maxSub[0] = nums[0]
        for i in xrange(1, len(nums)):
            maxSub[i] = max(maxSub[i-1], 0) + nums[i]
            res = max(res, maxSub[i])
        return res
```

# Maximum Product Subarray

> Find the contiguous subarray within an array (containing at least one number) which has the largest product.

> For example, given the array [2,3,-2,4],

> the contiguous subarray [2,3] has the largest product = 6.

```Python
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return
        maxProd, maxSub, minSub = nums[0], nums[0], nums[0]
        # maintain minSub to deal with negative value
        for indx in range(1, len(nums)):
            maxTmp = maxSub
            maxSub = max(max(maxSub * nums[indx], nums[indx]), minSub * nums[indx])
            minSub = min(min(maxTmp * nums[indx], nums[indx]), minSub * nums[indx])
            maxProd = max(maxProd, maxSub)
        return maxProd
```
