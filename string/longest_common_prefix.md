# Longest Common Prefix

> Write a function to find the longest common prefix string amongst an array of strings.

```Python
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs or "" in strs:
            return ""
        res = strs[0]
        for i, elem in enumerate(strs):
            for j in xrange(min(len(res), len(elem))):
                if res[j] != elem[j]:
                    res = res[:j]
                    break
                if j == len(elem)-1:
                    res = res[:j+1]
        return res
```
