# Generate Parentheses

> Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

> For example, given n = 3, a solution set is:

> ```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

```Python
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        if n < 1: return []
        res = []
        self.getParen(res, "", n, 0)
        return res

    def getParen(self, res, sub, left, right):
        if left == 0 and right == 0:
            res.append(sub)
            return
        if left > 0:
            self.getParen(res, sub+"(", left-1, right+1)
        if right > 0:
            self.getParen(res, sub+")", left, right-1)
```
