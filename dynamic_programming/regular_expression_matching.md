# Regular Expression Matching

> Implement regular expression matching with support for '.' and '*'.

> ```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).
The function prototype should be:
bool isMatch(const char *s, const char *p)
Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

Recursive solution.

```Python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        if not p: return s == ''
        if len(p) > 1 and p[1] == '*':
            if len(p) > 3 and p[3] == '*' and p[2] == p[0]:
                return self.isMatch(s, p[2:])   # used to avoid LTE cases like a*a*a*a*a*a*a*a*a*
            tmp1 = self.isMatch(s, p[2:])   # x* matches zero
            tmp2 = s[1:] if len(s) > 1 else ''   # x* matches one or more
            return tmp1 or s != '' and (p[0] == s[0] or p[0] == '.') and self.isMatch(tmp2, p)
        else:
            tmp1 = s[1:] if len(s) > 1 else ''
            tmp2 = p[1:] if len(p) > 1 else ''
            return s != '' and (p[0] == s[0] or p[0] == '.') and self.isMatch(tmp1, tmp2)
```
