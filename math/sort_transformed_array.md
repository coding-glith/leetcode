# Sort Transformed Array

> Given a sorted array of integers nums and integer values a, b and c. Apply a function of the form f(x) = ax2 + bx + c to each element x in the array.

> The returned array must be in sorted order.

> Expected time complexity: O(n)

> Example:

> ```
nums = [-4, -2, 2, 4], a = 1, b = 3, c = 5,
Result: [3, 9, 15, 33]
nums = [-4, -2, 2, 4], a = -1, b = 3, c = 5
Result: [-23, -5, 1, 7]
```

```Python
class Solution(object):
    def sortTransformedArray(self, nums, a, b, c):
        """
        :type nums: List[int]
        :type a: int
        :type b: int
        :type c: int
        :rtype: List[int]
        """
        if len(nums) < 1:
            return nums
        start, end, res = 0, len(nums)-1, []
        while start <= end:
            startVal = self.getVal(nums[start], a, b, c)
            endVal = self.getVal(nums[end], a, b, c)
            if a >= 0:
                if startVal >= endVal:
                    res.insert(0, startVal)
                    start += 1
                else:
                    res.insert(0, endVal)
                    end -= 1
            if a < 0:
                if startVal >= endVal:
                    res.append(endVal)
                    end -= 1
                else:
                    res.append(startVal)
                    start += 1
        return res

    def getVal(self, x, a, b, c):
        return a*x*x + b*x + c
```
