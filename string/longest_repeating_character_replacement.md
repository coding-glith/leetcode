# Longest Repeating Character Replacement](longest_repeating_character_replacement.md)

> Given a string that consists of only uppercase English letters, you can replace any letter in the string with another letter at most k times. Find the length of a longest substring containing all repeating letters you can get after performing the above operations.

> Note:

> Both the string's length and k will not exceed 104.

> Example 1:

> ```
Input:
s = "ABAB", k = 2
Output:
4
Explanation:
Replace the two 'A's with two 'B's or vice versa.
```

> Example 2:

> ```
Input:
s = "AABABBA", k = 1
Output:
4
Explanation:
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```

```Python
class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        if not s: return 0
        most, start, res, charDict = s[0], 0, 1, {s[0]: 1}
        for i in xrange(1, len(s)):
            if s[i] in charDict:
                charDict[s[i]] += 1
            else:
                charDict[s[i]] = 1
            if charDict[s[i]] >= charDict[most]: most = s[i]
            while len(s[start : i+1]) - charDict[most] > k:
                charDict[s[start]] -= 1
                start += 1
                if charDict[s[start]] == charDict[most]:
                    # update most
                    for key in charDict.keys():
                        if charDict[key] >= charDict[most]: most = key
            res = max(res, i+1-start)
        return res
```
