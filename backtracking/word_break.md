# Word Break II

> Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

> Return all such possible sentences.

> For example, given

> s = "catsanddog",

> dict = ["cat", "cats", "and", "sand", "dog"].

> A solution is ["cats and dog", "cat sand dog"].

Below solution is from leetcode [discussion](https://discuss.leetcode.com/topic/27855/my-concise-java-solution-based-on-memorized-dfs). The standard backtracking method will get time limit exceeded error because of two many trace back to same sub-problem. The idea in this solution is to use a dictionary to memorize the sub problem and its corresponding results.

```Python
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: Set[str]
        :rtype: List[str]
        """
        return self.dfs(s, wordDict, {})

    def dfs(self, s, wordDict, resMap):
        if s in resMap: return resMap[s]
        if not s: return [""]
        res = []
        for word in wordDict:
            if s[:len(word)] == word:
                sublist = self.dfs(s[len(word):], wordDict, resMap)
                for sub in sublist:
                    tmp = word + " " + sub if sub else word
                    res.append(tmp)
        resMap[s] = res
        return res
```

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
