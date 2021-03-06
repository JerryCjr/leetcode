### 310. Minimum Height Trees

For an undirected graph with tree characteristics, we can choose any node as the root. The result graph is then a rooted tree. Among all possible rooted trees, those with minimum height are called minimum height trees (MHTs). Given such a graph, write a function to find all the MHTs and return a list of their root labels.

Format
The graph contains n nodes which are labeled from 0 to n - 1. You will be given the number n and a list of undirected edges (each edge is a pair of labels).

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

**Example 1 :**
```
Input: n = 4, edges = [[1, 0], [1, 2], [1, 3]]

        0
        |
        1
       / \
      2   3 

Output: [1]
```

**Example 2 :**
```
Input: n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

     0  1  2
      \ | /
        3
        |
        4
        |
        5 

Output: [3, 4]
```

**Note:**
- According to the definition of tree on Wikipedia: “a tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.”
- The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

**Solution**
```Python
class Solution(object):
    def findMinHeightTrees(self, n, edges):
        """
        :type n: int
        :type edges: List[List[int]]
        :rtype: List[int]
        """
        if n <= 2:
            return [i for i in range(n)]
        
        visited = [False] * n
        in_degrees = [0] * n
        e_m = {i: [] for i in range(n)}
        for e in edges:
            e_m[e[0]].append(e[1])
            e_m[e[1]].append(e[0])
            in_degrees[e[0]] += 1
            in_degrees[e[1]] += 1
        
        queue = []
        for i in range(n):
            if in_degrees[i] == 1:
                queue.append(i)
                visited[i] = True
        
        not_visited_node_size = n
        while not_visited_node_size > 2:
            size = len(queue)
            
            for _ in range(size):
                v = queue.pop(0)
                in_degrees[v] -= 1
                for neighbour in e_m[v]:
                    in_degrees[neighbour] -= 1
                    if not visited[neighbour] and in_degrees[neighbour] == 1:
                        queue.append(neighbour)
                        visited[neighbour] = True
            
            not_visited_node_size -= size
        
        return queue
```