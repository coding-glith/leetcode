# Sentence Screen Fitting

> Given a rows x cols screen and a sentence represented by a list of words, find how many times the given sentence can be fitted on the screen.

> Note:

> * A word cannot be split into two lines.

> * The order of words in the sentence must remain unchanged.

> * Two consecutive words in a line must be separated by a single space.

> * Total words in the sentence won't exceed 100.

> * Length of each word won't exceed 10.

> * 1 ≤ rows, cols ≤ 20,000.

> Example 1:

> ```
Input:
rows = 2, cols = 8, sentence = ["hello", "world"]
Output: 
1
Explanation:
hello---
world---
The character '-' signifies an empty space on the screen.
```

> Example 2:

> ```
Input:
rows = 3, cols = 6, sentence = ["a", "bcd", "e"]
Output: 
2
Explanation:
a-bcd- 
e-a---
bcd-e-
The character '-' signifies an empty space on the screen.
```

> Example 3:

> ```
Input:
rows = 4, cols = 5, sentence = ["I", "had", "apple", "pie"]
Output: 
1
Explanation:
I-had
apple
pie-I
had--
The character '-' signifies an empty space on the screen.
```

Solution from leetcode [discussion](https://discuss.leetcode.com/topic/62455/21ms-18-lines-java-solution).

The idea is to form a long string of sentence and then calculate the index of each row in the long string.

```Python
class Solution(object):
    def wordsTyping(self, sentence, rows, cols):
        """
        :type sentence: List[str]
        :type rows: int
        :type cols: int
        :rtype: int
        """
        s = " ".join(sentence) + " "
        start = 0
        for row in xrange(rows):
            start += cols
            if s[start % len(s)] == " ": start += 1    # deal with start with " "
            else:
                while start > 0 and s[(start-1) % len(s)] != " ": start -= 1   # deal with one word cannot fit in one line
        return start / len(s)
```

Straightforward solution, time limit exceeded.

```Python
class Solution(object):
    def wordsTyping(self, sentence, rows, cols):
        """
        :type sentence: List[str]
        :type rows: int
        :type cols: int
        :rtype: int
        """
        row, col, res = 0, 0, 0
        while row < rows:
            for i, word in enumerate(sentence):
                if len(word) > cols: return 0
                if col + len(word) < cols:
                    col += len(word) + 1
                elif col + len(word) == cols:
                    col = 0
                    row += 1
                    if row == rows: return res if i != len(sentence)-1 else res + 1
                else:
                    col = len(word) + 1
                    row += 1
                    if row == rows: return res
            res += 1
        return res
```
