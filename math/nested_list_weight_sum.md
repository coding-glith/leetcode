# Nested List Weight Sum

> Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

> Each element is either an integer, or a list -- whose elements may also be integers or other lists.

> Example 1:

> Given the list [[1,1],2,[1,1]], return 10. (four 1's at depth 2, one 2 at depth 1)

> Example 2:

> Given the list [1,[4,[6]]], return 27. (one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4*2 + 6*3 = 27)

```Python
# """
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# """
#class NestedInteger(object):
#    def isInteger(self):
#        """
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        :rtype bool
#        """
#
#    def getInteger(self):
#        """
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        :rtype int
#        """
#
#    def getList(self):
#        """
#        @return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        :rtype List[NestedInteger]
#        """

class Solution(object):
    def depthSum(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        return self.levelSum(nestedList, 1)

    def levelSum(self, nList, level):
        tmpSum = 0
        for elem in nList:
            if elem.isInteger():
                tmpSum += level * elem.getInteger()
            else:
                tmpSum += self.levelSum(elem.getList(), level+1)
        return tmpSum
```


# Nested List Weight Sum II

> Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

> Each element is either an integer, or a list -- whose elements may also be integers or other lists.

> Different from the previous question where weight is increasing from root to leaf, now the weight is defined from bottom up. i.e., the leaf level integers have weight 1, and the root level integers have the largest weight.

> Example 1:

> Given the list [[1,1],2,[1,1]], return 8. (four 1's at depth 1, one 2 at depth 2)

> Example 2:

> Given the list [1,[4,[6]]], return 17. (one 1 at depth 3, one 4 at depth 2, and one 6 at depth 1; 1*3 + 4*2 + 6*1 = 17)

```Python

```
