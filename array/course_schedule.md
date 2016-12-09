# Course Schedule

> There are a total of n courses you have to take, labeled from 0 to n - 1.

> Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

> Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

> For example:

> ```
2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.
2, [[1,0],[0,1]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

> Note:

> * The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

> Hints:

> * This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.

> * Topological Sort via DFS - A great video tutorial (21 minutes) on Coursera explaining the basic concepts of Topological Sort.

> * Topological sort could also be done via BFS.

BFS.

```Python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        courseList = [[] for _ in xrange(numCourses)] # list of course require i as prereq
        prerNum = [0] * numCourses  # number of prereq for course i
        for pair in prerequisites:
            prerNum[pair[0]] += 1
            courseList[pair[1]].append(pair[0])
        noPrerList = collections.deque()
        for i in xrange(numCourses):
            if prerNum[i] == 0: noPrerList.append(i)
        count = 0
        while noPrerList:
            course = noPrerList.popleft()  # take this course
            count += 1
            for i in courseList[course]:  # courses require above course as prereq
                prerNum[i] -= 1
                if prerNum[i] == 0: noPrerList.append(i)
        return count == numCourses
```

DFS.

```Python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        courseList = [[] for _ in xrange(numCourses)] # list of prereq courses for i
        visit = [0] * numCourses
        for pair in prerequisites:
            courseList[pair[0]].append(pair[1])

        def dfs(i):
            if visit[i] == -1: return False
            if visit[i] == 1: return True
            visit[i] = -1  # means cycle
            for pre in courseList[i]:
                if not dfs(pre): return False
            visit[i] = 1   # means no cycle
            return True
        
        for i in xrange(numCourses):
            if not dfs(i): return False
        return True
```

# Course Schedule II

> There are a total of n courses you have to take, labeled from 0 to n - 1.

> Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

> Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

> There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

> For example:

> ```
2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1]
4, [[1,0],[2,0],[3,1],[3,2]]
There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].
```

```Python
class Solution(object):
    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """
        courseList = [[] for _ in xrange(numCourses)] # list of course require i as prereq
        prerNum = [0] * numCourses  # number of prereq for course i
        for pair in prerequisites:
            prerNum[pair[0]] += 1
            courseList[pair[1]].append(pair[0])
        noPrerList = collections.deque()
        for i in xrange(numCourses):
            if prerNum[i] == 0: noPrerList.append(i)
        res, count = [], 0
        while noPrerList:
            course = noPrerList.popleft()  # take this course
            res.append(course); count += 1
            for i in courseList[course]:  # courses require above course as prereq
                prerNum[i] -= 1
                if prerNum[i] == 0: noPrerList.append(i)
        return res if count == numCourses else []
```
