# Wildcard Matching

> Implement wildcard pattern matching with support for '?' and '*'.

> ```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).
The function prototype should be:
bool isMatch(const char *s, const char *p)
Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
```

Recursive way. below solution failed for some cases, need to deal with time limit exceeded error.

example:

```
x.isMatch("abbabbbaabaaabbbbbabbabbabbbabbaaabbbababbabaaabbab", "*aabb***aa**a******aa*")
```

```Python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        if not p: return s == ''
        if not s:
            for i in xrange(len(p)):
                if p[i] != '*':
                    return False
            return True
        if p[-1] == '*':
            return self.isMatch(s[:-1], p) or self.isMatch(s, p[:-1])
        else:
            return (p[-1] == s[-1] or p[-1] == '?') and self.isMatch(s[:-1], p[:-1])
```
