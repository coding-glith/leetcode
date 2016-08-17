# Implement strStr()

> Implement strStr().

> Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Lot of solutions are implementing the "KMP algorithm", see explanation from [Wikipedia](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm).

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
