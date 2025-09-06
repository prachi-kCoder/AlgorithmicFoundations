# PRIMS-ALGORITHM 

- GREEDY STRATEGY TO USE PQ {to take up the all the unvisited nodes from `non-mst set` -> `mst-set` :
- Priority-Queue {use to get the lowest path upto and unvisited node}
- Keep track of vis[node] to avoid cycles .
- Consider better over `DENSE GREAPH` ad multiple connection are explored upto a node and the one with least cost is explored with other are discarded.
  ### Keep in mind vis a node only after adding in PQ {ie they've become a part of mst } and then check for next unvisited nodes :
- People usually get confused int 2 ways but they'rereally very diff :-


#### WRONG WAY :
- Here we are marking nodes vis even before consider them in the pq , ie they ' re not yet sorted as per their order in pq , PQ determines which node to be connected via the min_cost possible making the MST , but here marking nbr nodes vis[v] = true , here we're eleiminating the chance of reaching those v nodes with lower cost with other path we may encounter in the future with some other nodes .
```cpp
vis[0] = true ;
while (!pq.empty()) {
	auto p = pq.top(); pq.pop();
	int u = p.second ; int cost = p.first ;
	for (auto nbr : adj[u]) {
		int v = nbr.first ; int wt = nbr.second ;
		if (!vis[v]) {
			pq.push({wt , v});
		}
	}
}
```

###### Right Approch will be to check every u nodes coming out of PQ vis/ or not and if not then vis and join in the MST 
 ```cpp
while (!pq.empty()) {
	auto p = pq.top(); pq.pop();
	int u = p.second ; int cost = p.first ;
	if (vis[u]) continue ;
	vis[u] = true ;
	total += cost ;
	for (auto nbr : adj[u]) {
		int v = nbr.first ; int wt = nbr.second ;
		if (!vis[v]) {
			pq.push({wt , v});
		}
	}
}
```
### CODE SOLUTION :
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<pair<int,int>>> adj ;

int spanningTree(int V, vector<vector<int>>& edges) {
        vector<vector<pair<int,int>>> adj(V) ;
        
        for (vector<int> e : edges) {
            int u = e[0] ; int v = e[1] ; int wt = e[2] ;
            adj[u].push_back({v , wt});
            adj[v].push_back({u , wt});
        }
        
        priority_queue<pair<int,int>,vector<pair<int,int>>,greater<>> pq ;
        //minHeap based on cost 
        
        pq.push({0 , 0}) ;
        vector<bool> vis(V , false) ;
        int total = 0 ;
        
    
        while (!pq.empty()) {
            auto p = pq.top(); pq.pop();
            int cost = p.first ;
            int u = p.second ;
            if (vis[u]) continue;
            vis[u] = true ;
            total += cost ;
            
            for (auto nbr : adj[u]) {
                int v = nbr.first ; int wt = nbr.second ;
                if (!vis[v]) {
                    
                    pq.push({wt , v});
                }
            }
        }
        
        return total ;
    }


```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O( (V+E)*log(V))         |   As all edges are explored O(E), and take in PQ and each insertion into PS take O(logV), each node is papped at most once O(vlogV) {only if unvisited one } }|
| 🧠 SPACE |   O(v+e)         |   Adjacency list stores all edges, and priority queue can hold up to V nodes|
