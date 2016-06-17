# Largest Rectangle in Histogram

> Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

> ![alt text](http://www.leetcode.com/wp-content/uploads/2012/04/histogram.png)

> Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].

> ![alt text](http://www.leetcode.com/wp-content/uploads/2012/04/histogram_area.png)

> The largest rectangle is shown in the shaded area, which has area = 10 unit.

> For example,

> Given heights = [2,1,5,6,2,3],

> return 10.

The idea here is to use a stack, kept in ascending order, to do the tracking.
first, append 0 at the end of heights to serve as boundary case - everything will be pop out and calculated.
second, go through the heights list, make sure the values in the stack is in ascending order.
        Once a smaller value occured, this is the rightmost point current calculation can reach. So to calculate current top's maximum area: pop out current top, the new top is the leftmost point to reach, since it's a smaller value. Also, note that if stack becomes empty, the leftmost is the very begginning of heights list because those values are larger.

```Python
class Solution(object):
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        stack, maxArea, indx = [], 0, 0
        heights.append(0)    # append 0 as boundary case
        while indx < len(heights):
            if stack == [] or heights[indx] > heights[stack[len(stack)-1]]:
                stack.append(indx)    # keep stack in ascending order
                indx += 1
            else:  # once find smaller one, this indx is the rightmost point to be reached
                top = stack[len(stack)-1]
                stack.pop()
                if stack == []:  # bottom is the smallest, should add previous values in
                    maxArea = max(maxArea, heights[top] * indx)
                else:   # after pop out, current top is smaller than pop value, so it's the leftmost point
                    maxArea = max(maxArea, heights[top] * (indx-stack[len(stack)-1]-1))
        heights.pop()
        return maxArea
```
