# Maximum Subarray

> Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

> For example, given the array [−2,1,−3,4,−1,2,1,−5,4],

> he contiguous subarray [4,−1,2,1] has the largest sum = 6.

> More practice:

> If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

The idea here is that maxSub[indx] is the maximum sum from 0 to indx, and the value of indx should always be considered.

```Python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return
        maxSub = [0 for indx in range(len(nums))]
        maxSub[0] = nums[0]
        maxSum = nums[0]
        for indx in range(1, len(nums)):
            if maxSub[indx-1] > 0:
                maxSub[indx] = nums[indx] + maxSub[indx-1]
            else:
                maxSub[indx] = nums[indx]
            maxSum = max(maxSum, maxSub[indx])
        return maxSum
```

# Maximum Product Subarray

> Find the contiguous subarray within an array (containing at least one number) which has the largest product.

> For example, given the array [2,3,-2,4],

> the contiguous subarray [2,3] has the largest product = 6.

```Python

```
