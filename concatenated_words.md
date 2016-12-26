# Concatenated Words

> Given a list of words (without duplicates), please write a program that returns all concatenated words in the given list of words.

> A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.

> Example:

> ```
Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
             "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
             "ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
```

> Note:

> * The number of elements of the given array will not exceed 10,000

> * The length sum of elements in the given array will not exceed 600,000.

> * All the input string will only include lower case letters.

> * The returned elements order does not matter.

DFS solution from word break. go through the words and check if each word can be break into concatenate words from others. This solution is O(N^3). TLE.

```Python
class Solution(object):
    def findAllConcatenatedWordsInADict(self, words):
        """
        :type words: List[str]
        :rtype: List[str]
        """
        res = []
        for word in words:
            wordDict = set(words)
            wordDict.remove(word)
            if word and self.canBreak(word, wordDict):
                res.append(word)
        return res
    
    def canBreak(self, s, wordDict):
        flag = [False for _ in xrange(len(s)+1)]
        flag[0] = True
        for i in xrange(1, len(s)+1):
            for inner in xrange(i-1, -1, -1):
                if flag[inner] and s[inner:i] in wordDict:
                    flag[i] = True; break
        return flag[-1]
```
