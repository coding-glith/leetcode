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

dp solution

```Python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        # dp[row][col]: if s[0..row-1] matches p[0..col-1]
        dp = [[False for col in xrange(len(p)+1)] for row in xrange(len(s)+1)]
        dp[0][0] = True   # s == '' and p == ''
        # dp[row][0] = False because s != '' and p == ''
        for col in xrange(2, len(p)+1):
            dp[0][col] = dp[0][col-2] and p[col-1] == '*'
        
        for row in xrange(1, len(s)+1):
            for col in xrange(1, len(p)+1):
                if p[col-1] != '*':  # check previous string match and current case match
                    dp[row][col] = dp[row-1][col-1] and (p[col-1] == s[row-1] or p[col-1] == '.')
                else:              # match zero       match one or more ...                    and check for latter
                    dp[row][col] = dp[row][col-2] or (p[col-2] == s[row-1] or p[col-2] == '.') and dp[row-1][col]
        return dp[len(s)][len(p)]
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
