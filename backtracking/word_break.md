# Word Break II

> Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

> Return all such possible sentences.

> For example, given

> s = "catsanddog",

> dict = ["cat", "cats", "and", "sand", "dog"].

> A solution is ["cats and dog", "cat sand dog"].

Backtracking solution. Get time limit exceeded.

```Python
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: Set[str]
        :rtype: List[str]
        """
        res = []
        self.wbreak(res, '', s, wordDict, 0, 0)
        return res

    def wbreak(self, res, sub, s, wordDict, start, end):
        if start >= len(s):
            if end == len(s)-1:
                res.append(str(sub))
            return
        for i in xrange(start, len(s)):
            if s[start:i+1] in wordDict:
                sub = s[start:i+1] if not sub else sub + " " + s[start:i+1]
                self.wbreak(res, sub, s, wordDict, i+1, i)
                tmpList = sub.split(" ")[:-1]
                sub = " ".join(tmpList)
```
