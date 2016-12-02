# Longest Valid Parentheses

> Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

> For "(()", the longest valid parentheses substring is "()", which has length = 2.

> Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.

```Python
class Solution(object):
    def longestValidParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s: return 0
        res, stack = [0] * len(s), []
        for i in xrange(len(s)):
            if s[i] == "(": stack.append(i)
            else:
                if stack:
                    idx = stack.pop()
                    res[i] = res[idx-1] + i + 1 - idx
        return max(res)
```
