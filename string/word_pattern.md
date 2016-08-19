# Word Pattern

> Given a pattern and a string str, find if str follows the same pattern.

> Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

> Examples:

> * pattern = "abba", str = "dog cat cat dog" should return true.

> * pattern = "abba", str = "dog cat cat fish" should return false.

> * pattern = "aaaa", str = "dog cat cat dog" should return false.

> * pattern = "abba", str = "dog dog dog dog" should return false.

> Notes:

> You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

```Python
class Solution(object):
    def wordPattern(self, pattern, str):
        """
        :type pattern: str
        :type str: str
        :rtype: bool
        """
        return self.isValid(pattern, str.split(' ')) and self.isValid(str.split(' '), pattern)

    def isValid(self, p, s):
        if len(p) != len(s):
            return False
        mapDict = {}
        for i in xrange(len(p)):
            if p[i] not in mapDict:
                mapDict[p[i]] = s[i]
            else:
                if mapDict[p[i]] != s[i]:
                    return False
        return True
```
