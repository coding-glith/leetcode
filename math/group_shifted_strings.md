# Group Shifted Strings

> Given a string, we can "shift" each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep "shifting" which forms the sequence:

> ```
"abc" -> "bcd" -> ... -> "xyz"
```

> Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

> For example, given: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"], 

> A solution is:

> ```
[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
```

The idea is to calculate a unique pattern for each string, if they are the same, group them in the dictionary.

```Python
class Solution(object):
    def groupStrings(self, strings):
        """
        :type strings: List[str]
        :rtype: List[List[str]]
        """
        if len(strings) == 0:
            return []
        resultDict, result = {}, []
        for s in strings:
            if self.shift(s) not in resultDict:
                resultDict[self.shift(s)] = [s]
            else:
                resultDict[self.shift(s)] += [s]
        for i in resultDict:
            result.append(resultDict[i])
        return result
            

    def shift(self, s):
        res = ''
        for i in xrange(1, len(s)):
            diff = ord(s[i]) - ord(s[i-1])
            if diff < 0:  # deal with 'za', 'ab'
                diff += 26
            res += chr(ord('a')+diff) + ','
        return res
```
