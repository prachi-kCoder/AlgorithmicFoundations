# CourseSchedule-II
## (BFS - KAHN's Algorithm)
```cpp
class Solution {
public:
    vector<int> findOrder(int n, vector<vector<int>>& prereq) {
        vector<vector<int>> adj(n);
        vector<int> inDeg(n, 0);
        vector<int> res;

        // Build graph: b → a means a depends on b
        for (auto& e : prereq) {
            int a = e[0], b = e[1];
            adj[b].push_back(a);
            inDeg[a]++;
        }

        queue<int> q;
        for (int i = 0; i < n; i++) {
            if (inDeg[i] == 0) q.push(i);  // No prerequisites
        }

        while (!q.empty()) {
            int u = q.front(); q.pop();
            res.push_back(u);
            for (int v : adj[u]) {
                inDeg[v]--;
                if (inDeg[v] == 0) q.push(v);
            }
        }

        if (res.size() != n) return {};  // Cycle detected

        return res;
    }
};
```
###  Major confusion point i faced while in the soluion is  :
- [a,b] that is to do task 'a'  first do 'b'  : This sounds like (b->a) adj[b].push_back(a)  [b->a]  #here a depends over b
- But if this way if its done then inDeg of inDeg of 'b' is increased as we take up those course have inDeg = 0 in queue first which are actually those courses having no such course which can be done after them as they are directing to other courses
- As per the question we need to get the courses with no dependency to do any other before them so that we can do them first
- If this happens simple reverse the order made at the end (that's what i did ) so the the ones will be reaching through the directed nodes are the ones which should come before
## Or 
- Rather make the graph [a->b]  as adj[a].push_back(b)   That is after doing b we can do a ,
-  so inDeg of a in decreased while traversing in queue .

- ## Second thing that people often miss check is : Check for cycles in graph
- Because if the graph have any cycle we end up traversing the cycle & won't visit all the nodes any way
- Do check whether the inDeg of all the nodes are 0 at the end or not (Just to check all nodes reached ) if any node which inDegree > 0 then cycle exist !

## DFS 
```cpp
class Solution {
public:
    bool dfs(int node , vector<bool>& vis, vector<bool>& stk, vector<vector<int>>& adj , vector<int>& res) {
        vis[node] = true ;
        stk[node] = true ;
        for(int nbr : adj[node]) {
            if (!vis[nbr]) {
                if (!dfs(nbr , vis, stk , adj , res)) return false ;
            }else if (stk[nbr]) return false ;
        }
        stk[node] = false ;
        res.push_back(node) ;
        return true ;
    }
    vector<int> findOrder(int n, vector<vector<int>>& prereq) {
        vector<vector<int>> adj(n) ;
        for (vector<int> e : prereq) {
            int a = e[0] ; int b = e[1] ;
            // Before a do b ie a Depends over b (Stack up those dependencies in adj list for that to vis them first & get them in res{})
            adj[a].push_back(b) ;// a store its dependencies
        }
        vector<int> res ;
        vector<bool> vis(n, false) ;
        vector<bool> stk(n, false) ;
        for(int i = 0; i < n ; i++) {
            if (!vis[i]) {
                if (!dfs(i , vis , stk, adj, res)) return {} ;
            }
        }
        return res ;

    }
};
```
- Here in DFS we did adj[a].push_back(b)  [a->b] ie before a go and do DFS for b , ie what we do and get all those courses to be done before a , by doing dfs for the nbr's of a and then add a to the res !

# 🔍 Complexity Analysis

# BFS KAHN'S 
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V + E)     |  Adj List formation O(E) , Indegree traversal O(V) + BFS O(V+E)  |
| 🧠 SPACE |   O(V + V)      |   Indeg [], Adj[] , res[]|

# DFS 
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V + E)     |  Adj List formation O(E) ,  DFS O(V+E) |
| 🧠 SPACE |   O(V + V + V + v) = O(V)      |   Vis [], Stack[], Adj[] , res[]|
