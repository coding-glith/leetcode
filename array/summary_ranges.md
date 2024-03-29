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
        if not nums: return []
        res, start, end = [], nums[0], nums[0]
        nums.append(sys.maxint)
        for i in xrange(1, len(nums)):
            if nums[i] != nums[i-1] + 1:
                if end > start:
                    res.append(str(start) + "->" + str(end))
                else:
                    res.append(str(start))
                start = nums[i]
            end = nums[i]
        nums.pop()
        return res
```

# Missing Ranges

> Given a sorted integer array where the range of elements are [lower, upper] inclusive, return its missing ranges.

> For example, given [0, 1, 3, 50, 75], lower = 0 and upper = 99, return ["2", "4->49", "51->74", "76->99"].

```Python
class Solution(object):
    def findMissingRanges(self, nums, lower, upper):
        """
        :type nums: List[int]
        :type lower: int
        :type upper: int
        :rtype: List[str]
        """
        res, prev = [], lower-1
        nums.append(upper+1)
        for elem in nums:
            if elem == prev + 2:
                res.append(str(elem-1))
            if elem > prev + 2:  # +2 is because of the +1 and -1 below
                res.append(str(prev+1)+"->"+str(elem-1))
            prev = elem
        nums.pop()
        return res
```
