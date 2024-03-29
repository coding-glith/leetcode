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
        res, sDict, start, k = 0, {}, 0, 2
        for i in xrange(len(s)):
            if s[i] not in sDict:
                while len(sDict.keys()) >= k:
                    sDict[s[start]] -= 1
                    if sDict[s[start]] == 0:
                        sDict.pop(s[start], None)
                    start += 1
                sDict[s[i]] = 1
            else:
                sDict[s[i]] += 1
            res = max(res, i+1-start)
        return res
```

# Longest Substring with At Most K Distinct Characters

> Given a string, find the length of the longest substring T that contains at most k distinct characters.

> For example, Given s = “eceba” and k = 2,

> T is "ece" which its length is 3.

Same as above, just add a check for k <= 0.

```Python
class Solution(object):
    def lengthOfLongestSubstringKDistinct(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        if k <= 0: return 0
        res, sDict, start = 0, {}, 0
        for i in xrange(len(s)):
            if s[i] not in sDict:
                while len(sDict.keys()) >= k:
                    sDict[s[start]] -= 1
                    if sDict[s[start]] == 0:
                        sDict.pop(s[start], None)
                    start += 1
                sDict[s[i]] = 1
            else:
                sDict[s[i]] += 1
            res = max(res, i+1-start)
        return res   
```
