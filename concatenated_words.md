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

Trie Solution. Trie is dictionary of dictionary, check letter in dictionary is fast. O(N^2) ???

```Python
class Solution(object):
    def findAllConcatenatedWordsInADict(self, words):
        """
        :type words: List[str]
        :rtype: List[str]
        """
        result = []
        # creat trie: O(N*len(word))
        self.trie = Trie()
        for word in words:
            self.trie.insert(word)
        # search trie: O(N*??)
        for word in words:
            if self.search(word): result.append(word)
        return result

    def search(self, word):
        node = self.trie.root
        for i, letter in enumerate(word):
            node = node.children.get(letter)
            if not node: return False
            suffix = word[i+1:]
            # check suffix is word: self.trie.search(suffix)
            # check suffix can break: self.search(suffix)
            if node.isWord and (self.trie.search(suffix) or self.search(suffix)):
                return True
        return False
            

class TrieNode(object):
    def __init__(self):
        self.children = {}
        self.isWord = False

class Trie(object):
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for letter in word:
            child = node.children.get(letter)
            if not child:
                child = TrieNode()
                node.children[letter] = child
            node = child
        node.isWord = True

    def search(self, word):
        node = self.root
        for letter in word:
            node = node.children.get(letter)
            if not node: return False
        return node.isWord
```

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
