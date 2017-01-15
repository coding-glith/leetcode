# Implement strStr()

> Implement strStr().

> Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

O(m+n). implementation of the "KMP algorithm", see explanation from [Wikipedia](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm). and leetcode [discussion](https://discuss.leetcode.com/topic/30471/java-and-python-solution-using-kmp-with-o-m-n-time-complexity)

go through haystack and check needle from the start need O(mn).

```Python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        # returnToIdx: when meeting mismatch at curIdx, return to returnToIdx[curIdx]
        # the value before preIdx and curIdx is matched
        returnToIdx = [-1] * len(needle)
        preIdx, curIdx = -1, 0
        while curIdx < len(needle)-1:
            if preIdx == -1 or needle[preIdx] == needle[curIdx]:
                curIdx += 1; preIdx += 1
                returnToIdx[curIdx] = preIdx
            else:  # if no match, go back to the match where preIdx is curIdx
                preIdx = returnToIdx[preIdx]
        i, curIdx = 0, 0
        while i < len(haystack) and curIdx < len(needle):
            if curIdx == -1 or haystack[i] == needle[curIdx]:
                i += 1; curIdx += 1
            else:
                curIdx = returnToIdx[curIdx]
        return i - curIdx if curIdx == len(needle) else -1
```

```Python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if needle not in haystack:
            return -1
        else:
            return haystack.find(needle)
```
