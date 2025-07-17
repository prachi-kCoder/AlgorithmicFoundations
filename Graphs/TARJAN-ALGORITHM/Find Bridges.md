# FIND CRITICAL CONNECTIONS / BRIDGES IN AN UNDIRECTED GRAPH 
## TARJAN'S ALGORITHM 
### INTUITION : 
- Keep a track of low[] : lowest Time of Insertion of any node 
- Keep a track of tin[] :  Time of Insertion of any node
- Do DFS for unvisited nodes and update the lowest time of insertion of nbr with yourself so that to keep the lowest way to reach any node
- For visited no (But not par) : Do update the lowest time , because a visited neigbour , not parent then obviously the cycle formation and there is possibility that the visited node could have made call for me , rather that another as they also have an edge connected .
- ## tin[u] < low[v]  then  the edge is bridge ?
- - Because if if tin if u {par}, v[nbr] , if tin[u] < low[v] ie the nbr is visited via the par only so if the edge got disconnected the graph will get split in components !
 
  - 
```cpp
class Solution {
public:
    int timer = 1 ;
    void dfs(int node , int par, vector<bool>& vis,int low[], int tin[], vector<int> adj[], vector<vector<int>>& bridges) {
        vis[node] = true ;
        low[node] = tin[node] = timer ;
        timer++ ;

        for (int v  : adj[node]) {
            if (v == par) continue ;
            if (!vis[v]) {
                dfs(v , node , vis , low, tin , adj , bridges);

                low[node] = min(low[node] , low[v]) ;

                if (tin[node] < low[v]){
                    bridges.push_back({node , v});
                }
            }else { // if vis
                low[node] = min(low[node] , low[v]) ;
            }
        }
    }
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        vector<int> adj[n];
        vector<vector<int>> bridges ;
        for (vector<int> e : connections) {
            adj[e[0]].push_back(e[1]);
            adj[e[1]].push_back(e[0]);
        }
        vector<bool> vis(n , false) ;
        int low[n];
        int tin[n];
        dfs(0 , -1 , vis , low , tin , adj, bridges) ;
        return bridges ;
    }
};
```

# 🔍 Complexity Analysis

| 🔢 METRIC |	✅ COMPLEXITY	|📌 WHY?|
|-----------|-------------|------------|
| 🧭 TIME  | O(V + E)	  |DFS visits each vertex and explores each edge once.  |
| 🧠 SPACE | O(V + E)	|Adjacency list (O(V + E)), plus arrays low, tin, vis (O(V)). Recursion stack in DFS is O(V) in worst case.|
