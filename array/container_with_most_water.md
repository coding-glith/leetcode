# Container With Most Water

> Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

> Note: You may not slant the container.

> For example: given [2,3,2]

> ```
    |
|   |   |
|___|___|
```

```Python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        res, start, end = 0, 0, len(height)-1
        while start <= end:
            res = max(res, min(height[start], height[end])*(end-start))
            if height[start] < height[end]:
                start += 1
            else:
                end -= 1
        return res
```
