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

# Shortest Word Distance II

> This is a follow up of Shortest Word Distance. The only difference is now you are given the list of words and your method will be called repeatedly many times with different parameters. How would you optimize it?

> Design a class which receives a list of words in the constructor, and implements a method that takes two words word1 and word2 and return the shortest distance between these two words in the list.

> For example,

> Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

> Given word1 = “coding”, word2 = “practice”, return 3.

> Given word1 = "makes", word2 = "coding", return 1.

> Note:

> You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

```Python
class WordDistance(object):
    def __init__(self, words):
        """
        initialize your data structure here.
        :type words: List[str]
        """
        self.words = {}  # a dictionary of words followed by its indices
        for i, w in enumerate(words):
            self.words[w] = self.words.get(w, []) + [i]
        

    def shortest(self, word1, word2):
        """
        Adds a word into the data structure.
        :type word1: str
        :type word2: str
        :rtype: int
        """
        idx1, idx2 = self.words[word1], self.words[word2]
        a, b, res = 0, 0, float('inf')
        while a < len(idx1) and b < len(idx2):
            res = min(res, abs(idx1[a] - idx2[b]))
            if idx1[a] > idx2[b]:
                b += 1
            else:
                a += 1
        return res
        
        


# Your WordDistance object will be instantiated and called as such:
# wordDistance = WordDistance(words)
# wordDistance.shortest("word1", "word2")
# wordDistance.shortest("anotherWord1", "anotherWord2")  
```

# Shortest Word Distance III

> This is a follow up of Shortest Word Distance. The only difference is now word1 could be the same as word2.

> Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

> word1 and word2 may be the same and they represent two individual words in the list.

> For example,

> Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

> Given word1 = “makes”, word2 = “coding”, return 1.

> Given word1 = "makes", word2 = "makes", return 3.

> Note:

> You may assume word1 and word2 are both in the list.

```Python
class Solution(object):
    def shortestWordDistance(self, words, word1, word2):
        """
        :type words: List[str]
        :type word1: str
        :type word2: str
        :rtype: int
        """
        res, idx1, idx2, flag = len(words), -1, -1, 0
        for i, val in enumerate(words):
            if val == word1 and val == word2:
                if flag % 2 == 0:
                    idx1 = i
                else:
                    idx2 = i
                flag += 1
            if val == word1 and val != word2:
                idx1 = i
            if val == word2 and val != word1:
                idx2 = i
            if idx1 != -1 and idx2 != -1:
                res = min(res, abs(idx1 - idx2))
        return res
```
