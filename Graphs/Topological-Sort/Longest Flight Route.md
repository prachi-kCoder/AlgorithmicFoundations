# Longest Flight Route 
##### Things to keep in mind :-
            - Kahn’s algorithm guarantees that every node is processed only after all its dependencies (incoming edges) are resolved.
            - Even if dp[u] == -1, we must process u to decrement in_deg[v] for its neighbors. This ensures that no node is skipped, and all potential paths are explored.
            - This is crucial because some nodes might not be part of the longest path, but their presence is necessary to unlock other nodes.
  
#### DP Logic: Tracks Optimal Path Lengths
            - dp[v] < dp[u] + 1 ensures that we only update dp[v] and par[v] if we find a longer path to v through u.
            - This selective update is what gives DP its power: it filters out suboptimal paths and retains only the best one.
            - The par[v] = u assignment is what enables path reconstruction later.
### Point of Mistake :
    - DP logic should not interfere with Kahn’s mechanics. Even if dp[u] == -1, we still reduce in_deg[v] and push v into the queue when in_deg[v] == 0.
    - This separation ensures that topological order is preserved, and DP updates happen only when valid.
  
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
 
int main() {
	int n , m ;
	cin >> n >> m ;
	adj.resize(n) ;
	
	vector<int> in_deg(n, 0) ;
	vector<int> par(n , -1) ;
	vector<int> dp(n , -1) ; // max_nodes covered to reach ith node 
	for (int j = 0 ;  j < m ; j++) {
	    int a , b ;
	    cin >> a >> b ;
	    a-- ; b-- ;
	    adj[a].push_back(b);
	    in_deg[b]++ ;
	}
	queue<int> q ;
	q.push(0) ;
	dp[0] = 1 ;
	for (int i = 1 ; i < n ; i++) { // leaving 0
	    if (in_deg[i] == 0){
	        q.push(i) ;
	    }
	}
	
	while (!q.empty()) {
	    int u = q.front(); q.pop();
	   // if (dp[u] == -1) continue    ;
	    
	    for (int v : adj[u]) {
	        in_deg[v]-- ;
	        if (dp[u] != -1 && dp[v] < dp[u] + 1) {
	           dp[v] = dp[u] + 1 ;
	           par[v] = u ;
	           
	        }
	        if (in_deg[v] == 0 ){
    	         q.push(v) ;
    	    }
	        
	    }
	}
 
	if(dp[n-1] == -1) {
	    cout << "IMPOSSIBLE" << endl ;
	} else {
	    vector<int> res ;
    	int c = n-1 ;
    	while (c != -1) {
    	    res.push_back(c); 
    	    c = par[c] ;
    	}
    	reverse(res.begin() , res.end()) ;
    	cout << res.size() << endl ;
    	for (int node : res) {
    	    cout << (node + 1) << " " ;
    	}
    	cout << endl ;
    }
	
	
	return  0 ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V+E)     | Kahn's Algo (BFS) , Adj Formation    |
| 🧠 SPACE |   O(V+E)     |    Adj , Parent Arr , in_deg arr , Queue       |
