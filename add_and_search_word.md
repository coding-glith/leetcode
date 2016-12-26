# Add and Search Word - Data structure design

> Design a data structure that supports the following two operations:

> ```
void addWord(word)
bool search(word)
search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.
```

> For example:

> ```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

> Note:

> You may assume that all words are consist of lowercase letters a-z.

```Python
class WordDictionary(object):
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.trie = Trie()
        

    def addWord(self, word):
        """
        Adds a word into the data structure.
        :type word: str
        :rtype: void
        """
        self.trie.insert(word)
        

    def search(self, word):
        """
        Returns if the word is in the data structure. A word could
        contain the dot character '.' to represent any one letter.
        :type word: str
        :rtype: bool
        """
        if not word: return False
        return self.traverse(self.trie.root, word)

    
    def traverse(self, node, word):
        if not node: return False
        if not word: return node.isWord
        if word[0] != ".":
            child = node.children.get(word[0])
            if not child: return False
            if self.traverse(child, word[1:]): return True
        else:
            for child in node.children:
                if self.traverse(node.children[child], word[1:]): return True
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
        

# Your WordDictionary object will be instantiated and called as such:
# wordDictionary = WordDictionary()
# wordDictionary.addWord("word")
# wordDictionary.search("pattern")
```
