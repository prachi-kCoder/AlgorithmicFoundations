# Friend Circles  or NO. PROVINCES
- https://leetcode.com/problems/number-of-provinces/description/
```cpp
class Solution {
public:
    vector<int> adj[201] ;
    void dfs(int node , vector<bool>& vis) {
        vis[node] = true ;
        for (int nbr : adj[node]) {
            if (vis[nbr] ) continue ;
            dfs(nbr ,vis) ;
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
## BFS : use ques rather that recusvive calls
```cpp
void bfs(int node , vector<bool>& vis)  {
        queue<int> q ;
        q.push(node) ;
        while (!q.empty()){
            int curr = q.front(); q.pop();
            vis[curr] = true ;
            for (int nbr : adj[curr]) {
                  if (!vis[nbr]){
                   q.push(nbr) ;
                }
            }
        }
    }
```
# 🔍 Complexity Analysis
## DFS
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n*n) + O(n)  | Matrix Traversal + Vertex traversal (DFS) |
| 🧠 SPACE |  O(V + E )          | Vis O(N) + Adj List (O(E))|

## **BFS**
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n*n) + O(n)  | Matrix Traversal + Vertex traversal BFS |
| 🧠 SPACE |  O(V + E )          | Vis O(N) + Adj List (O(E))|**
