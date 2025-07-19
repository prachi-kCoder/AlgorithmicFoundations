## FIND HAMILTONIAN PATH EXIST OR NOT 

- Hamiltonial Path is the path in a graph to visit all nodes exactly once  , (Don't Confuse with Hamiltonian Cycle which is a path visiting all nodes and reaching back to the startNode)

- NOTE :This code if code the graph with node starting at [1 ,n ] ie is why the full mask is taken as (1<<(n+1) - 2) to exclude the 0th bit , in case the graph has node [0,n-1] Full mask = (1<<n) to check for all nodes from 0 to n-1 are visited or not
  

```cpp
  class Solution {
  public:
    bool check(int n, int m, vector<vector<int>> edges) {
        vector<vector<int>> adj(n+1) ;
        for (vector<int> e : edges) {
            // for 1 based indexing
            adj[e[0]].push_back(e[1]);
            adj[e[1]].push_back(e[0]);
        }
        queue<pair<int,int>> q ;
        vector<vector<int>> dp(n+1 , vector<int>((1 << n+1) , INT_MAX)) ;
        for (int i = 1 ; i <= n ; i++) {
            q.push({i , (1<<i)});
            dp[i][1<<i] = 1 ;
        }
        while (!q.empty()) {
            int sz = q.size();
            for ( int i = 0; i < sz ; i++ ) {
                auto c = q.front(); q.pop();
                int u = c.first ; int mask = c.second ;
                int fullMask = (1 << (n + 1)) - 2;  // Excludes bit 0 (since index starts at 1)
                if (mask == fullMask) return true;
                
                for (int v : adj[u]) {
                    if (u == v) continue ;// selfLoop
                    if (mask&(1<<v)) {
                        dp[v][1<<v] = false ;
                        continue ;
                    }
                    int newMask = (mask|(1<<v)) ;
                    if (dp[v][newMask] == INT_MAX) {// unexplored
                        q.push({v ,newMask}) ; 
                    }
                }
            }
        }
        
        return false ;
    }
  };
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  | O(V + E + V*(2^V)) |  Adj List formation + For all v nodes {2^V} visiting states|
| 🧠 SPACE |  O(V + E + V*(2^V))  | Adj List + DP[nodes][mask]|






