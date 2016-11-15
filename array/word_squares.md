# Valid Word Square

> Given a sequence of words, check whether it forms a valid word square.

> A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

> Note:

> * The number of words given is at least 1 and does not exceed 500.

> * Word length will be at least 1 and does not exceed 500.

> * Each word contains only lowercase English alphabet a-z.

> Example 1:

> ```
Input:
[
  "abcd",
  "bnrt",
  "crmy",
  "dtye"
]
Output:
true
Explanation:
The first row and first column both read "abcd".
The second row and second column both read "bnrt".
The third row and third column both read "crmy".
The fourth row and fourth column both read "dtye".
Therefore, it is a valid word square.
```

> Example 2:

> ```
Input:
[
  "abcd",
  "bnrt",
  "crm",
  "dt"
]
Output:
true
Explanation:
The first row and first column both read "abcd".
The second row and second column both read "bnrt".
The third row and third column both read "crm".
The fourth row and fourth column both read "dt".
Therefore, it is a valid word square.
```

> Example 3:

> ```
Input:
[
  "ball",
  "area",
  "read",
  "lady"
]
Output:
false
Explanation:
The third row reads "read" while the third column reads "lead".
Therefore, it is NOT a valid word square.
```

Instead of checking all the conditions of whether the value exists or not, use dummy value '*' to mark the array so that array index in managable.

```Python
class Solution(object):
    def validWordSquare(self, words):
        """
        :type words: List[str]
        :rtype: bool
        """
        maxLen = len(words)
        for i in xrange(len(words)):
            if len(words[i]) > maxLen:
                maxLen = len(words[i])
        # create a matrix fill the empty entries with '*'
        tmp = [['*' for col in xrange(maxLen)] for row in xrange(maxLen)]
        for row in xrange(len(words)):
            for col in xrange(len(words[row])):
                tmp[row][col] = words[row][col]
        # check
        for k in xrange(maxLen):
            col = k - 1
            while col >= 0:
                if tmp[k][col] != tmp[col][k]:
                    return False
                col -= 1
        return True
```

# Word Squares

> Given a set of words (without duplicates), find all word squares you can build from them.

> A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

> For example, the word sequence ["ball","area","lead","lady"] forms a word square because each word reads the same both horizontally and vertically.

> ```
b a l l
a r e a
l e a d
l a d y
```

> Note:

> * There are at least 1 and at most 1000 words.

> * All words will have the exact same length.

> * Word length is at least 1 and at most 5.

> * Each word contains only lowercase English alphabet a-z.

> Example 1:

> ```
Input:
["area","lead","wall","lady","ball"]
Output:
[
  [ "wall",
    "area",
    "lead",
    "lady"
  ],
  [ "ball",
    "area",
    "lead",
    "lady"
  ]
]
Explanation:
The output consists of two word squares. 
The order of output does not matter (just the order of words in each word square matters).
```

> Example 2:

> ```
Input:
["abat","baba","atan","atal"]
Output:
[
  [ "baba",
    "abat",
    "baba",
    "atan"
  ],
  [ "baba",
    "abat",
    "baba",
    "atal"
  ]
]
Explanation:
The output consists of two word squares. 
The order of output does not matter (just the order of words in each word square matters).
```

The idea is to try every word at the first row, then search for the rest based on square requirement. Here we are using trie for fast search for words.

```Python
class Solution(object):
    def wordSquares(self, words):
        """
        :type words: List[str]
        :rtype: List[List[str]]
        """
        if not words: return [[]]
        trie = self.buildTrie(words)
        res = []
        self.dfs(res, [], trie, len(words[0]), '')
        return res        

    def traverseTrie(self, res, trie):
        for key in trie:
            if key == "_end_":
                res.append(trie[key])
                return
            else:
                self.traverseTrie(res, trie[key])
        
    def getWords(self, trie, prefix):
        for char in prefix:
            if char not in trie: return []
            trie = trie[char]   # traverse the trie with prefix
        res = []
        self.traverseTrie(res, trie)   # get all words under current position
        return res

    def dfs(self, res, sub, trie, wordLen, prefix):
        candidates = self.getWords(trie, prefix)   # a pool with words satisfy prefix
        for word in candidates:
            if len(sub) == wordLen - 1:
                res.append(list(sub+[word]))
                continue   # continue with other candidates
            newPrefix = ''
            for w in sub+[word]:
                newPrefix += w[len(sub)+1]
            self.dfs(res, sub+[word], trie, wordLen, newPrefix)

    def buildTrie(self, words):
        trie = {}
        for word in words:
            tmp = trie
            for char in word:
                if char not in tmp:
                    tmp[char] = {}
                tmp = tmp[char]
            tmp["_end_"] = word
        return trie
```
