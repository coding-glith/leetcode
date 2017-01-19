# Clone Graph

> Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.

> OJ's undirected graph serialization:

> Nodes are labeled uniquely.

> We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.

> As an example, consider the serialized graph {0,1,2#1,2#2,2}.

> The graph has a total of three nodes, and therefore contains three parts as separated by #.

> * First node is labeled as 0. Connect node 0 to both nodes 1 and 2.

> * Second node is labeled as 1. Connect node 1 to node 2.

> * Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.

> Visually, the graph looks like the following:

> ```
       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```

BFS. Besides general bfs, need to maintain a hash table to map the original node with new node, this is the key to link the node with its neighbors.

```Python
# Definition for a undirected graph node
# class UndirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []

class Solution:
    # @param node, a undirected graph node
    # @return a undirected graph node
    def cloneGraph(self, node):
        if not node: return node
        nodeCopy = UndirectedGraphNode(node.label)
        nodeDict = {node: nodeCopy}
        level = [node]
        while level:
            n = level.pop(0)
            for nb in n.neighbors:
                if nb not in nodeDict:   # nb not visited
                    nbCopy = UndirectedGraphNode(nb.label)
                    nodeDict[nb] = nbCopy
                    nodeDict[n].neighbors.append(nbCopy)
                    level.append(nb)
                else:   # nb visited, no need to create new node copy, append to neighbor list
                    nodeDict[n].neighbors.append(nodeDict[nb])
        return nodeCopy
```

DFS iteratively. The only difference to BFS above is that BFS uses queue while DFS uses stack.

```Python
# Definition for a undirected graph node
# class UndirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []

class Solution:
    # @param node, a undirected graph node
    # @return a undirected graph node
    def cloneGraph(self, node):
        if not node: return node
        nodeCopy = UndirectedGraphNode(node.label)
        nodeDict = {node: nodeCopy}
        stack = [node]
        while stack:
            n = stack.pop()
            for nb in n.neighbors:
                if nb not in nodeDict:
                    nbCopy = UndirectedGraphNode(nb.label)
                    nodeDict[nb] = nbCopy
                    nodeDict[n].neighbors.append(nbCopy)
                    stack.append(nb)
                else:
                    nodeDict[n].neighbors.append(nodeDict[nb])
        return nodeCopy
```

DFS recursively.

```Python
# Definition for a undirected graph node
# class UndirectedGraphNode:
#     def __init__(self, x):
#         self.label = x
#         self.neighbors = []

class Solution:
    # @param node, a undirected graph node
    # @return a undirected graph node
    def cloneGraph(self, node):
        if not node: return node
        nodeCopy = UndirectedGraphNode(node.label)
        nodeDict = {node: nodeCopy}
        self.dfs(node, nodeDict)
        return nodeCopy
    
    def dfs(self, n, nodeDict):
        for nb in n.neighbors:
            if nb not in nodeDict:
                nbCopy = UndirectedGraphNode(nb.label)
                nodeDict[nb] = nbCopy
                nodeDict[n].neighbors.append(nbCopy)
                self.dfs(nb, nodeDict)
            else:
                nodeDict[n].neighbors.append(nodeDict[nb])
```
