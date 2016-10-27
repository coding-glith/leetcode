# One Edit Distance

> Given two strings S and T, determine if they are both one edit distance apart.

```Python
class Solution(object):
    def isOneEditDistance(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        for i in xrange(min(len(s), len(t))):
            if s[i] != t[i]:
                if len(s) == len(t):
                    return s[i+1:] == t[i+1:] if i < len(s)-1 else True
                elif len(s) > len(t):
                    return s[i+1:] == t[i:]
                else:
                    return s[i:] == t[i+1:]
        return abs(len(s)-len(t)) == 1
```
