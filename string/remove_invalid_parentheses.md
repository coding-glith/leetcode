# Remove Invalid Parentheses

> Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

> Note: The input string may contain letters other than the parentheses ( and ).

> Examples:

> ```
"()())()" -> ["()()()", "(())()"]
"(a)())()" -> ["(a)()()", "(a())()"]
")(" -> [""]
```

DFS solution. See leetcode [discussion](https://discuss.leetcode.com/topic/34875/easy-short-concise-and-fast-java-dfs-3-ms-solution).

This problem can also be solve using BFS solution but much slower. The idea is remove one "(" or ")" to see if has valid results, otherwise move to the next level of removing two characters.

```Python
class Solution(object):
    def removeInvalidParentheses(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        res = []
        self.remove(res, s, 0, 0, ["(", ")"])
        return res

    def remove(self, res, s, traverse, removePos, checkOrder):
        count = 0
        for i in xrange(traverse, len(s)):
            if s[i] == checkOrder[0]: count += 1
            if s[i] == checkOrder[1]: count -= 1
            if count >= 0: continue
            # when count < 0, find unmatched pattern
            for j in xrange(removePos, i+1):
                # check the range from previously checked remove position to current
                # remove the first appearance of ")"
                if s[j] == checkOrder[1] and (j == removePos or s[j-1] != checkOrder[1]):
                    self.remove(res, s[:j]+s[j+1:], i, j, checkOrder)
            # once remove current unmatched parentheses
            # go back to previous level and continue checking later string
            return
        if checkOrder[0] == "(":
            # in case "((()(()", so for each string
            # need to check from left to right, then from right to left
            self.remove(res, s[::-1], 0, 0, checkOrder[::-1])
        else: res.append(s[::-1])
```
