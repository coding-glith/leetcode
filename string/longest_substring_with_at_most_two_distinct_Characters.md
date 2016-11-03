# Longest Substring with At Most Two Distinct Characters

> Given a string, find the length of the longest substring T that contains at most 2 distinct characters.

> For example, Given s = “eceba”,

> T is "ece" which its length is 3.

```Python
class Solution(object):
    def lengthOfLongestSubstringTwoDistinct(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s: return 0
        start, end, res, charDict = 0, 0, 1, {s[0]: 1}
        for i in xrange(1, len(s)):
            if s[i] not in charDict.keys():
                while len(charDict.keys()) >= 2:
                    charDict[s[start]] -= 1
                    if charDict[s[start]] == 0:
                        charDict.pop(s[start])
                    start += 1
                charDict[s[i]] = 1
            else:
                charDict[s[i]] += 1
            end = i
            res = max(res, end+1-start)
        return res
```
