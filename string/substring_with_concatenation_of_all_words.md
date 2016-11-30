# Substring with Concatenation of All Words

> You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.

> For example, given:

> ```
s: "barfoothefoobarman"
words: ["foo", "bar"]
You should return the indices: [0,9].
(order does not matter).
```

The good part of this solution is it's idea of the index. The run time complexity is O(len(s)len(words[0])/len(wors)). So it will pass the case when words = ['a', 'a', 'a', 'a', and more].

```Python

```

My original solution. But this solution gets time limit exceeded error. The run time complexity is O(len(s)len(words)).

```
"barfoothefoobarman", ["bar", "foo"], check:
 barfoo   -> attach to results
  arf     -> once unsatisfy, break current loop
   rfo
    foothefoo   -> check more than number of words, break current loop
     oot
      oth
       the
        hef
         efo
          foobar   -> attach to results
           oob
```

```Python
class Solution(object):
    def findSubstring(self, s, words):
        """
        :type s: str
        :type words: List[str]
        :rtype: List[int]
        """
        if not words or len(s) < len(words) * len(words[0]): return []
        res, wordLen, wordNum, wordDict = [], len(words[0]), len(words), {}
        num, dic, flag = len(words), {}, False
        for word in words:
            if word not in wordDict: wordDict[word] = 1; dic[word] = 1
            else: wordDict[word] += 1; dic[word] += 1
        for i in xrange(len(s)-wordLen+1):
            if s[i:i+wordLen] not in wordDict: continue
                
            checkIdx = i
            while checkIdx < len(s)-wordLen+1 and wordNum != 0:  # continue search for the rest
                if s[checkIdx:checkIdx+wordLen] not in wordDict: break
                if wordDict[s[checkIdx:checkIdx+wordLen]] > 0: wordNum -= 1
                wordDict[s[checkIdx:checkIdx+wordLen]] -= 1
                if wordDict[s[checkIdx:checkIdx+wordLen]] < 0:
                    # set i after where s[checkIdx:checkIdx+wordLen] appear last time
                    tmp = checkIdx - wordLen
                    while tmp >= 0:
                        if s[tmp:tmp+wordLen] == s[checkIdx:checkIdx+wordLen]:
                            i = tmp + wordLen - 1
                            break
                        tmp -= wordLen
                    ###
                    flag = True; break
                checkIdx += wordLen
                
            if wordNum == 0 and not flag:  # reset and start a new round
                res.append(i)
            wordNum, wordDict, flag = num, dict(dic), False
        return res
```
