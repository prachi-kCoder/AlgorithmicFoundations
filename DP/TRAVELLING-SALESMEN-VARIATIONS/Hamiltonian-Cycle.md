## HAMILTONIAN CYCLE 
#### INTUITION  :
- Starting from any node get a path which ends at the same node without visiting the any other node more than 1 time and all nodes are to be visited ! Just Do BFS and keep a track of visited states using bitmask and check whether u came back to the same starting node or not ?
  
```cpp
#include <bits/stdc++.h>
using namespace std;
// start & end at same vertex 
bool HamiltonianCycle(int n ,vector<vector<int>>& edges) {
    if (n <= 1) return true ;
    
    vector<vector<int>> adj(n) ;
    
    for (vector<int> e : edges) {
        adj[e[0]].push_back(e[1]);
        adj[e[1]].push_back(e[0]);
    }
	vector<vector<int>> dp(n , vector<int>((1<<n), -1));
	
	queue<vector<int>> q ;
	for (int i = 0; i < n ; i++) {
	    vector<int> e = {i , i, (1<<i)} ;// to keep startNode
	    q.push(e);
	    dp[i][(1<<i)] = 0 ;
	}

	while (!q.empty()) {
	    int sz = q.size();
	    
	    for (int i = 0; i < sz ; i++) {
	        vector<int> p = q.front() ; q.pop();
	        int startNode = p[0] ;
	        int u = p[1] ; int msk = p[2] ;
	        if (msk == ((1<<n)-1)) {
	            for (int v : adj[u]) {
	                if (v == startNode) return true ;
	            }
	            dp[u][msk] = 0 ;
	        }else {
    	        for (int v : adj[u]) {
    	            if (msk&(1<<v)) continue ; // already visited node 
    	            int nxtMsk = (msk|(1<<v));
    	            if (dp[v][nxtMsk] == -1) {
    	                dp[v][nxtMsk] = 1 ;
    	                q.push({startNode,v , nxtMsk});
    	            }
    	        }    
	        }
	    }
	
	}
    return false ;
}
int main() {
	vector<vector<int>> edges = {{0,1},{0,5},{1,2},{1,4},{1,5},{2,3},{3,4},{4,5}};
	int n = 6 ; //[0,5]
	cout << HamiltonianCycle(n ,edges) << endl ;
}
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  | O(V + E + V*(2^V)) |  Adj List formation + For all v nodes {2^V} visiting states|
| 🧠 SPACE |  O(V + E + V*(2^V))  | Adj List + DP[nodes][mask]|
