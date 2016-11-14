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
