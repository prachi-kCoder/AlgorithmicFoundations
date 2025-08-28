# PRIMS-ALGORITHM 
- GREEDY STRATEGY TO USE PQ {to take up the all the unvisited nodes from `non-mst set` -> `mst-set` :
- Priority-Queue {use to get the lowest path upto and unvisited node}
- Keep track of vis[node] to avoid cycles .
- Consider better over `DENSE GREAPH` ad multiple connection are explored upto a node and the one with least cost is explored with other are discarded.
- 

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<pair<int,int>>> adj ;
int mst_cost(int n , vector<vector<int>>& edges) {
    adj.resize(n) ;// 0-5 
	for (vector<int> e : edges) {
	    int u  = e[0] ;
	    int v  = e[1] , wt  = e[2] ;
	    u-- , v-- ;
	    adj[u].push_back({v,wt});
	    adj[v].push_back({u,wt});
	}
    int cost = 0 ;
    
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<>> pq ;
    pq.push({0,0});
    vector<bool> vis(n,false) ;
    
    while (!pq.empty()) {
        auto [curr,u] = pq.top() ; pq.pop();
        if (vis[u]) continue ;
        vis[u] = true ;
        cost += curr ;
        
        for (auto [v,wt] : adj[u]) {
            if (!vis[v]) {
                pq.push({wt , v}) ;
            }
        }
    }
    
    return cost ;
}
int main() {
	// Prim's Algorithm : MST 
	 vector<vector<int>> edges = {
        {1,2,5},{1,3,1},{2,3,2},{2,6,12},
        {3,6,1},{3,4,10},{3,5,3},{4,5,6}
    };
	int n = 6 ;// 1-6 
	
	cout << mst_cost(n,edges) << endl ;

}

```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O( (V+E)*log(V))         |   As all edges are explored O(E), and take in PQ and each insertion into PS take O(logV), each node is papped at most once O(vlogV) {only if unvisited one } }|
| 🧠 SPACE |   O(v+e)         |   Adjacency list stores all edges, and priority queue can hold up to V nodes|
