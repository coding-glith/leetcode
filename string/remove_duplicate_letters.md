# Remove Duplicate Letters

> Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

> Example:

> ```
Given "bcabc"
Return "abc"

Given "cbacdcbc"
Return "acdb"
```

```Python
class Solution(object):
    def removeDuplicateLetters(self, s):
        """
        :type s: str
        :rtype: str
        """
        if not s: return s
        counts = collections.Counter(s)
        checkIdx = 0
        for i, val in enumerate(s):
            if val < s[checkIdx]: checkIdx = i
            counts[val] -= 1
            if counts[val] == 0: break
        
        return s[checkIdx] + self.removeDuplicateLetters(s[checkIdx+1:].replace(s[checkIdx], ""))
```
