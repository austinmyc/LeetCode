Link to Q: https://leetcode.com/problems/build-a-matrix-with-conditions/

## Question
You are given a positive integer k. You are also given:

a 2D integer array rowConditions of size n where `rowConditions[i]` = `\[above_i, below_i]`, belowi, and
a 2D integer array colConditions of size m where  `colConditions[i]` = `[left_i, right_i]`.
The two arrays contain integers from 1 to k.

You have to build a k x k matrix that contains each of the numbers from 1 to k exactly once. The remaining cells should have the value 0.

The matrix should also satisfy the following conditions:

The number abovei should appear in a row that is strictly above the row at which the number below i appears for all i from 0 to n - 1.
The number lefti should appear in a column that is strictly left of the column at which the number righti appears for all i from 0 to m - 1.
Return any matrix that satisfies the conditions. If no answer exists, return an empty matrix.

## Code
```python
class Solution:
    def buildMatrix(self, k: int, rowConditions: List[List[int]], colConditions: List[List[int]]) -> List[List[int]]:
        
        #topological sort

        def dfs(src, adj, visit, path, order):
            if src in path:
                return False
            if src in visit:
                return True
            visit.add(src)
            path.add(src)
            for n in adj[src]:
                if not dfs(n, adj, visit, path, order):
                    return False
            path.remove(src)
            order.append(src)
            return True

        def topo(edges):
            adj=defaultdict(list)
            for f, t in edges:
                adj[f].append(t)
            
            visit, path=set(), set()
            order=[]
            for src in range(1, k+1):
                if not dfs(src, adj, visit, path, order):
                    return []
            return order[::-1]
        
        row_order=topo(rowConditions)
        col_order=topo(colConditions)
        if not row_order or not col_order:
            return []
        row_map={val: i for i, val in enumerate(row_order)}
        col_map={val: i for i, val in enumerate(col_order)}

        res=[[0]*k for _ in range(k)]

        for cur in range(1, k+1):
            r, c = row_map[cur], col_map[cur]
            res[r][c]=cur
        return res
```
