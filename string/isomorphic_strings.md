# Isomorphic Strings

> Given two strings s and t, determine if they are isomorphic.

> Two strings are isomorphic if the characters in s can be replaced to get t.

> All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

> For example,

> Given "egg", "add", return true.

> Given "foo", "bar", return false.

> Given "paper", "title", return true.

> Note:

> You may assume both s and t have the same length.

```Python
class Solution(object):
    def isIsomorphic(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        return self.isValid(s, t) and self.isValid(t, s)

    def isValid(self, s, t):
        mapDict = {}
        for i in xrange(len(s)):
            if s[i] not in mapDict:
                mapDict[s[i]] = t[i]
            else:
                if t[i] != mapDict[s[i]]:
                    return False
        return True
```
