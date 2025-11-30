# Shortest-Path-Reconstruction

- Try Here : https://www.algopath.ai/problems/trip-to-algoland
- IMPORTANT POINT
- 🧠 Why par[s] = -2 is clever ?? 
- In your code, par[v] = -1 is used to mark unvisited nodes. So if you didn't assign a special value to par[s], then s = 0 (i.e., the first node) would be indistinguishable from an unvisited node. That could cause two problems:
- Cycle confusion: If there's a cycle that leads back to node 0, and par[0] == -1, the BFS might treat it as unvisited and revisit it, which is incorrect.
- Path reconstruction ambiguity: During the backtracking phase, you need a clear stopping condition. If par[s] == -1, the loop might terminate prematurely or misinterpret the path.


```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n , m ;
    cin >> n >> m ;
    vector<vector<int>> adj(n) ;
    // vector<int> indeg(n,0) ;
    for (int j = 0 ; j < m ; j++) {
        int u , v ;
        cin >> u >> v ;
        u-- , v-- ;
        adj[u].push_back(v) ; 
    }

    int s , t ;
    cin >> s >> t ;
    if (s == t) {
        cout << 0 << endl ;
        return 0 ;
    }
    s-- , t-- ;

    queue<int> q ;
    q.push(s);
    vector<int> par(n, -1) ;
    par[s] = -2 ;// ie any path cycle should not come back to node 0
    bool found = false ;
    while (!q.empty()) {
        int curr = q.front(); q.pop();
        if (curr == t) {
            found = true ;
            break ;
        }
        for (int nbr : adj[curr]) {
            if (par[nbr] == -1) {
                par[nbr] = curr ;
                q.push(nbr) ;
            }
        }
    }
    if (!found) {
        cout << "Impossible" << endl ;
    }else {
        vector<pair<int,int>> path ;
        int u = t ;
        while (par[u] != -2) {
            path.push_back({par[u] , u}) ;
            u = par[u] ;
        }
        reverse(path.begin() , path.end()) ;
        cout << path.size() << endl ;
        for (pair<int,int> p : path) {
            cout << (p.first+1) << " " << (p.second + 1)<< endl ;
        }
    }

    return 0;
}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(V+E)     | BFS for shortest path , in worst case we may need to vis all nodes and edges |
| 🧠 SPACE |  o(V+E)         | Adj List , Par Array |

