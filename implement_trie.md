# Implement Trie (Prefix Tree)

> Implement a trie with insert, search, and startsWith methods.

> Note:

> You may assume that all inputs are consist of lowercase letters a-z.

```Python
class TrieNode(object):
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.children = {}
        self.isWord = False
        

class Trie(object):

    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: void
        """
        node = self.root
        for letter in word:
            child = node.children.get(letter)
            if not child:
                child = TrieNode()
                node.children[letter] = child
            node = child
        node.isWord = True
        

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        node = self.root
        for letter in word:
            child = node.children.get(letter)
            if not child: return False
            node = child
        return node.isWord
        

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie
        that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        node = self.root
        for letter in prefix:
            child = node.children.get(letter)
            if not child: return False
            node = child
        return self.traverse(node)
    
    def traverse(self, node):
        if not node: return False
        if node.isWord: return True
        for child in node.children:
            if self.traverse(node.children[child]): return True
        return False
        

# Your Trie object will be instantiated and called as such:
# trie = Trie()
# trie.insert("somestring")
# trie.search("key")
```
