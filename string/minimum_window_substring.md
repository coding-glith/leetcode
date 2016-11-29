# Minimum Window Substring

> Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

> For example,

> ```
S = "ADOBECODEBANC"
T = "ABC"
Minimum window is "BANC".
```

> Note:

> * If there is no such window in S that covers all characters in T, return the empty string "".

> * If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

The solution is to maintain a dictionary and flag to mark if all the target character are found.

ADOBECODEBANC

ADOBEC  -> put in result

 DOBEC
 
 DOBECODEBA  -> put in result again and again until
 
     CODEBA
     
      ODEBA
      
      ODEBANC   -> put in result again and again until
      
         BANC

```Python
class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if len(t) > len(s): return ""
        resStart, resEnd, checkStart = 0, 0, 0
        targetDict, missingNum = {}, len(t)
        # targetDict stores the frequence of each character in t
        for val in t:
            if val not in targetDict: targetDict[val] = 1
            else: targetDict[val] += 1
        # maintaining two window: [resStart:resEnd], [checkStart:i+1]
        for i in xrange(len(s)):
            if s[i] in targetDict:
                if targetDict[s[i]] > 0: missingNum -= 1
                targetDict[s[i]] -= 1
            while checkStart <= i and missingNum == 0:  # missingNum is the flag indicating if target are all found
                if resEnd == 0 or i - checkStart < resEnd - resStart:
                    resStart, resEnd = checkStart, i + 1
                if s[checkStart] in targetDict:
                    targetDict[s[checkStart]] += 1
                    if targetDict[s[checkStart]] > 0: missingNum += 1  # key part to break the loop
                checkStart += 1
        return s[resStart:resEnd]
```
