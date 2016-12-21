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

Using dictionary, check key in dictionary is O(1) complexity.

```Python
class Solution(object):
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """
        res, charDict = -1, {}
        for i in xrange(len(s)):
            if s[i] not in charDict:
                charDict[s[i]] = 1
                if res == -1: res = i
            else:
                charDict[s[i]] += 1
                if res != -1 and charDict[s[res]] > 1:
                    for j in xrange(res, i+1):
                        if charDict[s[j]] == 1:
                            res = j; break
                        else:
                            if j == i: res = -1
        return res
```
