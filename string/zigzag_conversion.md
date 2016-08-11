# ZigZag Conversion

> The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

> ```
P   A   H   N
A P L S I I G
Y   I   R
```

> And then read line by line: "PAHNAPLSIIGYIR"

> Write the code that will take a string and make this conversion given a number of rows:

> string convert(string text, int nRows);

> convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

The idea is to maintain a string list to store every row of the zigzag.

```Python
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if len(s) <= numRows:
            return s
        sList = ['' for i in xrange(numRows)]
        row, index = 0, 0
        while index < len(s):
            while row < numRows and index < len(s):
                sList[row] += s[index]
                index += 1
                row += 1
            if row == numRows:
                row -= 2
                while row > 0 and index < len(s):
                    sList[row] += s[index]
                    index += 1
                    row -= 1
        return ''.join(sList)
```
