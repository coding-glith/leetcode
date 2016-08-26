# Repeated DNA Sequences

> All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

> Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

> For example,

> ```
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",
Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```

```Python
class Solution(object):
    def findRepeatedDnaSequences(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        if len(s) < 11:
            return []
        sDict, res = {}, []
        for i in xrange(len(s)-9):
            if s[i:i+10] not in sDict:
                sDict[s[i:i+10]] = 1
            else:
                if s[i:i+10] not in res:
                    res.append(s[i:i+10])
        return res
```
