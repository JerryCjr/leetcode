### 210. Course Schedule II

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

**Example 1:**
```
Input: 2, [[1,0]] 
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished   
             course 0. So the correct course order is [0,1] .
```

**Example 2:**
```
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both     
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```

**Note:**

1. The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
2. You may assume that there are no duplicate edges in the input prerequisites.

**Solution**
```Python
class Solution(object):
    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """
        edge = {i: [] for i in range(numCourses)}
        in_degrees = [0 for i in range(numCourses)]
        
        for l in prerequisites:
            edge[l[1]].append(l[0])
            in_degrees[l[0]] += 1
        
        queue = []
        ans = []
        
        for i in range(numCourses):
            if in_degrees[i] == 0:
                queue.append(i)
        
        while len(queue) > 0:
            course = queue.pop(0)
            ans.append(course)
            
            for c in edge[course]:
                in_degrees[c] -= 1
                if in_degrees[c] == 0:
                    queue.append(c)
        
        return ans if len(ans) == numCourses else []
```