# Summary Ranges

> Given a sorted integer array without duplicates, return the summary of its ranges.

> For example, given [0,1,2,4,5,7], return ["0->2","4->5","7"].

```Python
class Solution(object):
    def summaryRanges(self, nums):
        """
        :type nums: List[int]
        :rtype: List[str]
        """
        if not nums:
            return []
        nums.append(float('inf'))  # to count the last element in
        res, s, count = [], str(nums[0]), 1
        for i in xrange(1, len(nums)):
            if nums[i] <= nums[i-1] + 1:
                count += 1
            else:
                if count > 1:
                    s += "->" + str(nums[i-1])
                    res.append(str(s))
                else:
                    res.append(str(s))
                s = str(nums[i])
                count = 1
        nums.pop()
        return res if res else [str(nums[i-1])]
```
