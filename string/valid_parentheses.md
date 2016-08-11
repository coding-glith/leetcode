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
        if len(s) == 0:
            return True
        sList = []
        for indx in xrange(len(s)):
            if s[indx] in ["(", "{", "["]:
                sList.append(s[indx])
            elif s[indx] == ")" and sList != [] and sList[-1] == "(":
                sList.pop()
            elif s[indx] == "]" and sList != [] and sList[-1] == "[":
                sList.pop()
            elif s[indx] == "}" and sList != [] and sList[-1] == "{":
                sList.pop()
            else:
                return False
        return True if sList == [] else False
```
