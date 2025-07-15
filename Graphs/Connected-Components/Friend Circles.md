# Friend Circles 
```cpp
class Solution {
public:
    vector<int> adj[201] ;
    void dfs(int node , int par, vector<bool>& vis) {
        vis[node] = true ;
        for (int nbr : adj[node]) {
            if (vis[nbr] || par == nbr) continue ;
            dfs(nbr , node , vis) ;
        }
    }
    int findCircleNum(vector<vector<int>>& con) {
        int comp = 0 ;
        int n = con.size();
        for (int i = 0;  i < n ; i++) {
            for (int j = i+1; j < n ; j++) {
                if (con[i][j] == 1) {
                    adj[i].push_back(j);
                    adj[j].push_back(i);
                }
            }
        }
        vector<bool> vis(n , false) ;
        for (int i = 0; i < n ; i++) {
            if (!vis[i]) {
                dfs(i , -1 , vis) ;
                comp++ ;
            }
        }
        return comp ;
    }
};
```
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n*n) + O(n)  | Matrix Traversal + Vertex traversal (DFS) |
| 🧠 SPACE |  O(V + E )          | Vis O(N) + Adj List (O(E))|
