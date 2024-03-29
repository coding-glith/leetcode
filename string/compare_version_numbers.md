# Compare Version Numbers

> Compare two version numbers version1 and version2.

> If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

> You may assume that the version strings are non-empty and contain only digits and the . character.

> The . character does not represent a decimal point and is used to separate number sequences.

> For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

> Here is an example of version numbers ordering:

> ```
0.1 < 1.1 < 1.2 < 13.37
```

```Python
class Solution(object):
    def compareVersion(self, version1, version2):
        """
        :type version1: str
        :type version2: str
        :rtype: int
        """
        v1, v2 = version1.split('.'), version2.split('.')
        flag, res = 1, 0
        if len(v1) > len(v2):
            tmp, v1, v2, flag = v1, v2, v1, -1
        for i in xrange(len(v1)):
            if int(v1[i]) > int(v2[i]):
                return flag
            elif int(v1[i]) < int(v2[i]):
                return -flag
            else:
                continue
        for j in xrange(i+1, len(v2)):
            if int(v2[j]) != 0:
                res = -1
        return flag * res
```
