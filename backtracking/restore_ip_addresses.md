# Restore IP Addresses

> Given a string containing only digits, restore it by returning all possible valid IP address combinations.

> For example:

> Given "25525511135",

> return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)

```Python
class Solution(object):
    def restoreIpAddresses(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        if len(s) < 4: return []
        res = []
        self.helper(s, 4, "", res, len(s))
        return res

    def helper(self, s, n, sub, res, stdlen):
        if len(s) < n or len(s) > 3 * n: return
        if n == 0 and len(sub[1:]) - 3 == stdlen:   # need to subtract 3 '.'s
            res.append(sub[1:])   # sub[0] = "."
            return
        for i in xrange(min(3, len(s))):
            if int(s[:(i+1)]) < 256:
                self.helper(s[(i+1):], n-1, sub+"."+str(int(s[:(i+1)])), res, stdlen)
                # the str(int()) is necessary, for case: "010010", don't allow 010.0.1.0
```
