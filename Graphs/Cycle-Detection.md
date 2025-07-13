# CYLCLE DETECTION 
```cpp
class Solution {
public:
    vector<int> adj[2001] ;
    bool dfs(int node , vector<bool>& vis , vector<bool>& stk) {
        vis[node] = true ;
        stk[node] = true ;
        for (int nbr : adj[node]) {
            if (vis[nbr] && stk[nbr]) return true ;
            if (!vis[nbr] && dfs(nbr , vis, stk)) return true ;
        }
        stk[node] = false ;
        return false ;
    }
    bool canFinish(int n, vector<vector<int>>& prereq) {
        // if no prereq then obviously we can take the course , but a cycle won't allow that a-> b , b->a 
        for (vector<int> e : prereq) {
            adj[e[0]].push_back(e[1]);
        }
        bool cycle = false ;
        vector<bool> vis(n,false ) ;
        vector<bool> stk(n,false ) ;
        for (int i = 0; i < n ; i++ ) {
            if (!vis[i]) {
                cycle = dfs(i ,vis, stk ) ;
                if (cycle) break ;
            }
        }

        return !cycle;
    }
};
```
# 🔍 Complexity Analysis

| METRIC   | COMPLEXCITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(V+E)   |  Adj  + CycleDetection Traversal to all n nodes|
|   🧠 SPACE | O(V+V+V)      | adj , vis, stk |

