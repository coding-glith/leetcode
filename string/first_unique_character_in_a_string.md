# First Unique Character in a String

> Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

> Examples:

> ```
s = "leetcode"
return 0.
s = "loveleetcode",
return 2.
```

> Note: You may assume the string contain only lowercase letters.

```Python
class Solution(object):
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s:
            return -1
        for i in xrange(len(s)):
            if s[i] not in s[i+1:] and s[i] not in s[:i]:
                return i
        return -1
```
