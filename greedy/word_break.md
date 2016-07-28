# Word Break

> Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

> For example, given

> s = "leetcode",

> dict = ["leet", "code"].

> Return true because "leetcode" can be segmented as "leet code".

```Python
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: Set[str]
        :rtype: bool
        """
        if s == "":
            return True
        result = [False for indx in xrange(len(s)+1)]
        result[0] = True
        for indx in xrange(1, len(s) + 1):
            for inner in xrange(indx - 1, -1, -1):
                if result[inner] and s[inner:indx] in wordDict:
                    result[indx] = True
                    break
        return result[len(s)]
```

# Word Break II

> Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

> Return all such possible sentences.

> For example, given

> s = "catsanddog",

> dict = ["cat", "cats", "and", "sand", "dog"].

> A solution is ["cats and dog", "cat sand dog"].

dp + dfs solution.

```Python
class Solution(object):
    def canBreak(self, s, wordDict):
        flag = [False for i in xrange(len(s) + 1)]
        flag[0] = True
        for indx in xrange(1, len(s) + 1):
            for inner in xrange(indx - 1, -1, -1):
                if flag[inner] and s[inner:indx] in wordDict:
                    flag[indx] = True
                    break
        return flag[len(s)]
        
    def getSentence(self, result, sentence, s, wordDict):
        if self.canBreak(s, wordDict):
            if len(s) == 0:
                result.append(str(sentence[1:]))
            for indx in xrange(1, len(s) + 1):
                if s[:indx] in wordDict:
                    self.getSentence(result, sentence+" "+s[:indx], s[indx:], wordDict)
        
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: Set[str]
        :rtype: List[str]
        """
        if s == "":
            return [""]
        result = []
        self.getSentence(result, "", s, wordDict)
        return result
```
