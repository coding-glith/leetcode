# Valid Parentheses

> Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

> The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

```Python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        for i in xrange(len(s)):
            if s[i] in (")", "]", "}"):
                top = stack.pop() if stack else ""
                if not top or (top == "(" and s[i] != ")") or \
                   (top == "[" and s[i] != "]") or \
                   (top == "{" and s[i] != "}"): return False
            else: stack.append(s[i])
        return True if not stack else False
```
