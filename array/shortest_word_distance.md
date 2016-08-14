# Shortest Word Distance

> Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

> For example,

> Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

> Given word1 = “coding”, word2 = “practice”, return 3.

> Given word1 = "makes", word2 = "coding", return 1.

> Note:

> You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

```Python
class Solution(object):
    def shortestDistance(self, words, word1, word2):
        """
        :type words: List[str]
        :type word1: str
        :type word2: str
        :rtype: int
        """
        if len(words) < 2 or word1 == word2:
            return -1
        result, prev1, prev2 = len(words), -1, -1
        for i, word in enumerate(words):
            if word == word1:
                prev2 = i
            if word == word2:
                prev1 = i
            if prev1 != -1 and prev2 != -1:
                result = min(result, abs(prev1 - prev2))
        return result
```
