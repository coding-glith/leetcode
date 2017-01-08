# Simplify Path

> Given an absolute path for a file (Unix-style), simplify it.

> For example,

> ```
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
```

> Corner Cases:

> * Did you consider the case where path = "/../"?

> * In this case, you should return "/".

> * Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".

> * In this case, you should ignore redundant slashes and return "/home/foo".

```Python
class Solution(object):
    def simplifyPath(self, path):
        """
        :type path: str
        :rtype: str
        """
        pathList = path.split("/")
        stack = []
        for val in pathList:
            if val == "..":
                if stack:
                    stack.pop()
            elif val and val != ".":
                stack.append(val)
        return "/" + "/".join(stack)
```
