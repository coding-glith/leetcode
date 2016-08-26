# Sparse Matrix Multiplication

> Given two sparse matrices A and B, return the result of AB.

> You may assume that A's column number is equal to B's row number.

> Example:

> ```
A = [
  [ 1, 0, 0],
  [-1, 0, 3]
]
B = [
  [ 7, 0, 0 ],
  [ 0, 0, 0 ],
  [ 0, 0, 1 ]
]
     |  1 0 0 |   | 7 0 0 |   |  7 0 0 |
AB = | -1 0 3 | x | 0 0 0 | = | -7 0 3 |
                  | 0 0 1 |
```

Need to add check for zero, because sparse matrix mostly contains 0s, by adding this check will save a lot of time.

```Python
class Solution(object):
    def multiply(self, A, B):
        """
        :type A: List[List[int]]
        :type B: List[List[int]]
        :rtype: List[List[int]]
        """
        res = [[0] * len(B[0]) for i in xrange(len(A))]
        for i, row in enumerate(A):
            for j, elemA in enumerate(row):
                if elemA:
                    for ii, elemB in enumerate(B[j]):
                        if elemB:
                            res[i][ii] += elemA * elemB
        return res
```

My original method, get "Time Limit Exceeded" error.

```Python
class Solution(object):
    def multiply(self, A, B):
        """
        :type A: List[List[int]]
        :type B: List[List[int]]
        :rtype: List[List[int]]
        """
        res, Bcol = [[0] * len(B[0]) for i in xrange(len(A))], []
        for i in xrange(len(B[0])):
            tmp = []
            for j in xrange(len(B)):
                tmp.append(B[j][i])
            Bcol.append(tmp)
        for row in xrange(len(A)):
            for col in xrange(len(Bcol)):
                res[row][col] = self.helper(A[row], Bcol[col])
        return res

    def helper(self, a, b):
        # this is multiply a * b'
        if len(a) != len(b):
            return []
        res = 0
        for i in xrange(len(a)):
            res += a[i] * b[i]
        return res
```
