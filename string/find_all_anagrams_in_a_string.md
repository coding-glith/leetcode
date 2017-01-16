# Find All Anagrams in a String

> Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

> Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

> The order of output does not matter.

> Example 1:

> ```
Input:
s: "cbaebabacd" p: "abc"
Output:
[0, 6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

> Example 2:

> ```
Input:
s: "abab" p: "ab"
Output:
[0, 1, 2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

```Python
class Solution(object):
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        if not p or len(p) > len(s): return []
        res, pBase = [], {}
        for i in xrange(len(p)):
            if p[i] not in pBase: pBase[p[i]] = 1
            else: pBase[p[i]] += 1
        pDict, start, count = dict(pBase), 0, 0
        for i in xrange(len(s)):
            if s[i] in pDict and pDict[s[i]] > 0:
                count += 1; pDict[s[i]] -= 1
                if count == len(p):
                    res.append(start)
                    pDict[s[start]] += 1; count -= 1; start += 1
            else:
                if s[i] not in pDict:
                    pDict, start, count = dict(pBase), i + 1, 0
                else:
                    while pDict[s[start]] != pDict[s[i]]:
                        pDict[s[start]] += 1
                        if pDict[s[start]] > 0: count -= 1
                        start += 1
                    start += 1
        return res
```

Staightforward solution, O(mn). Time limit exceeded.

```Python
class Solution(object):
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        result = []
        for i in xrange(len(s)-len(p)+1):
            if collections.Counter(s[i:i+len(p)]) == collections.Counter(p):
                result.append(i)
        return result
```
