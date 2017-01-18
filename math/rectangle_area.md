# Rectangle Area

> Find the total area covered by two rectilinear rectangles in a 2D plane.

> Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

> ![alt text](https://leetcode.com/static/images/problemset/rectangle_area.png)

> Assume that the total area is never beyond the maximum possible value of int.

Need to be really careful with different cases to determine if overlap or not. The basic idea is check the second rectangle at left or right, then check if it's above, below or far away in the x-axis.

```Python
class Solution(object):
    def computeArea(self, A, B, C, D, E, F, G, H):
        """
        :type A: int
        :type B: int
        :type C: int
        :type D: int
        :type E: int
        :type F: int
        :type G: int
        :type H: int
        :rtype: int
        """
        area = abs(A-C) * abs(B-D) + abs(E-G) * abs(F-H)
        if E >= C or F >= D or H <= B or G <= A:
            return area
        else:
            return area - abs(max(A,E)-min(C,G)) * abs(max(B,F)-min(D,H))
```
