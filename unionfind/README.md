# Union Find

> * [Number of Connected Components in an Undirected Graph](NumberofConnectedComponentsinanUndirectedGraph.md), add countHead.

> * [Number of Islands I/II](../array/number_of_islands.md), one dimensional idArray or use {} to implement idArray.

### Weighted Quick Union with Path Compression

Keep the tree almost flat. O(logN)

```Python
class WeightedQuickUnionPathCompression(object):
    def __init__(self, N):
        self.idArray = [i for i in xrange(N)]
        self.sizeArray = [1] * N

    def root(self, i):
        while self.idArray[i] != i:
            self.idArray[i] = self.idArray[self.idArray[i]]
            i = self.idArray[i]
        return i

    def connected(self, p, q):
        return self.root(p) == self.root(q)

    def union(self, p, q):
        i, j = self.root(p), self.root(q)
        if i == j: return
        if self.sizeArray[i] < self.sizeArray[j]:
            self.idArray[i] = j
            self.sizeArray[j] += self.sizeArray[i]
        else:
            self.idArray[j] = i
            self.sizeArray[i] += self.sizeArray[j]
```

### Quick Union

```Python
class QuickUnion(object):
    def __init__(self, N):
        self.idArray = [i for i in xrange(N)]

    def root(self, i):
        while self.idArray[i] != i:
            i = self.idArray[i]
        return i

    def connected(self, p, q):
        return self.root(p) == self.root(q)

    def union(self, p, q):
        self.idArray[self.root(p)] = self.root(q)
```

### Quick Find

```Python
class QuickFind(object):
    def __init__(self, N):
        self.idArray = [i for i in xrange(N)]

    def connected(self, p, q):
        return self.idArray[p] == self.idArray[q]

    def union(self, p, q):
        prevPid = self.idArray[p]
        for i, idVal in enumerate(self.idArray):
            if idVal == prevPid:
                self.idArray[i] = self.idArray[q]
```
