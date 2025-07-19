## HAMILTONIAN CYCLE 
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
