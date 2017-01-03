# Graph Valid Tree

> Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

> For example:

> ```
Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.
Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.
```

> Hint:

> * Given n = 5 and edges = [[0, 1], [1, 2], [3, 4]], what should your return? Is this case a valid tree?

> * According to the definition of tree on Wikipedia: “a tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.”

> * Note: you can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

```Python
class Solution(object):
    def validTree(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: bool
        """
        if n == 0: return True
        UF = UnionFind(n)
        for i, node in enumerate(edges):
            if not UF.union(node[0], node[1]): return False
        return UF.countHead == 1

class UnionFind(object):
    def __init__(self, N):
        self.idArray = [i for i in xrange(N)]
        self.sizeArray = [1] * N
        self.countHead = N

    def root(self, i):
        while self.idArray[i] != i:
            self.idArray[i] = self.idArray[self.idArray[i]]
            i = self.idArray[i]
        return i

    def connected(self, p, q):
        return self.root(p) == self.root(q)

    def union(self, p, q):
        i, j = self.root(p), self.root(q)
        if i == j: return False
        if self.sizeArray[i] < self.sizeArray[j]:
            self.idArray[i] = j
            self.sizeArray[j] += self.sizeArray[i]
        else:
            self.idArray[j] = i
            self.sizeArray[i] += self.sizeArray[j]
        self.countHead -= 1
        return True
```
