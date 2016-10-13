# Generalized Abbreviation

> Write a function to generate the generalized abbreviations of a word.

> Example:

> Given word = "word", return the following list (order does not matter):

> ```
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```

```Python
class Solution(object):
    def generateAbbreviations(self, word):
        """
        :type word: str
        :rtype: List[str]
        """
        res = []
        self.getAbbr(res, "", 0, 0, word)
        return res

    def getAbbr(self, res, sub, idx, count, word):
        if idx == len(word):
            res.append(sub + str(count) if count > 0 else sub)
            return
        self.getAbbr(res, sub, idx + 1, count + 1, word)
        self.getAbbr(res, sub + (str(count) if count > 0 else "") + word[idx], idx + 1, 0, word)
```
