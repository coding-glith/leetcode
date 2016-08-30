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
    def generateParenthesis(self, n, o=0):
        """
        :type n: int
        :rtype: List[str]
        """
        if n > 0 and o >= 0:
            return ['(' + p for p in self.generateParenthesis(n-1, o+1)] + \
                   [')' + p for p in self.generateParenthesis(n, o-1)]
        return [')' * o] if n == 0 else []
```
