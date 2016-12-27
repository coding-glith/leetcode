# Palindrome Pairs

> Given a list of unique words, find all pairs of distinct indices (i, j) in the given list, so that the concatenation of the two words, i.e. words[i] + words[j] is a palindrome.

> Example 1:

> ```
Given words = ["bat", "tab", "cat"]
Return [[0, 1], [1, 0]]
The palindromes are ["battab", "tabbat"]
```

> Example 2:

> ```
Given words = ["abcd", "dcba", "lls", "s", "sssll"]
Return [[0, 1], [1, 0], [3, 2], [2, 4]]
The palindromes are ["dcbaabcd", "abcddcba", "slls", "llssssll"]
```

At first, think of using Trie structure, but haven't figure out how to deal with empty string, prefix and suffix. This solution use dictionary to find out the word and its index. And for each word, go through all the letter, check current prefix and suffix. O(Nk) complexity.

```Python
class Solution(object):
    def palindromePairs(self, words):
        """
        :type words: List[str]
        :rtype: List[List[int]]
        """
        def isPalindrome(word):
            return word == word[::-1]
        wordsDict = {word: i for i, word in enumerate(words)}
        result = []
        for i, word in enumerate(words):
            for checkIdx in xrange(len(word)+1):
                if isPalindrome(word[:checkIdx]):
                    if word[checkIdx:][::-1] != word and word[checkIdx:][::-1] in wordsDict:
                        result.append([wordsDict[word[checkIdx:][::-1]], i])
                if checkIdx != len(word) and isPalindrome(word[checkIdx:]):
                    if word[:checkIdx][::-1] != word and word[:checkIdx][::-1] in wordsDict:
                        result.append([i, wordsDict[word[:checkIdx][::-1]]])
        return result
```
