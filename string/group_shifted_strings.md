# Group Shifted Strings

> Given a string, we can "shift" each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep "shifting" which forms the sequence:

> "abc" -> "bcd" -> ... -> "xyz"

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

```Python
class Solution(object):
    def groupStrings(self, strings):
        """
        :type strings: List[str]
        :rtype: List[List[str]]
        """
        result = {}
        for s in strings:
            key = "0"
            for i in xrange(len(s)-1):
                diff = ord(s[i+1]) - ord(s[i])
                if diff < 0: diff += 26
                key += str(diff)
            if key not in result:
                result[key] = [s]
            else:
                result[key].append(s)
        return result.values()
```
