# Get-Diameter of Graph Type Tree

## BFS APPROACH :
```cpp
#include <bits/stdc++.h>
using namespace std;
// get the farthest node to get the Diameter
int bfs(int startNode , int n, const vector<vector<int>>& adj){
    queue<int> q;
    q.push(startNode) ;
    vector<int> dist(n , 0) ;
    vector<bool> vis(n , false) ;
    int farthest = -1 ;
    int mxDist = 0;
    
    while (!q.empty()) {
        int curr = q.front() ; q.pop();
        vis[curr] = true ;
        
        for (int nbr : adj[curr]) {
            if (!vis[nbr]) {
                dist[nbr] = dist[curr] + 1 ;
                q.push(nbr) ;
                
                if (dist[nbr] > mxDist) {
                    mxDist = dist[nbr] ;
                    farthest = nbr ;
                }
            }
        }
    }
    
    return farthest ;
    
}
vector<int> getDia(int n, vector<vector<int>>& adj) {
    if (n == 1) return {0} ;
    
    int farthest = bfs(0 , n , adj);
    
    queue<int> q ;
    q.push(farthest) ;
    vector<int> dist(n , 0 );
    vector<int> par(n );
    par[farthest] = -1 ;
    
    vector<bool> vis(n , false );
    int end = -1 ;
    
    while (!q.empty()) {
        int u = q.front() ;  q.pop() ;
        vis[u] = true ;
        
        for (int v : adj[u]) {
            if (!vis[v]) {
                par[v] = u ;
                dist[v] = dist[u] + 1 ;
                q.push(v) ;
                
                if (end == -1 || dist[end] < dist[v]) {
                    end = v ;
                    
                }
            }
        }
    }
    
    // reconstruct 
    vector<int> finalDia ;
    while (end != -1) {
        finalDia.push_back(end) ;
        end = par[end] ;
    }
    reverse(finalDia.begin(), finalDia.end());
    
    return finalDia ;
}
int main() {
    int n = 14 ;//[0-13] treeNodes
	vector<vector<int>> edges = {{13,12},{12,0},{0,1},{1,3},{3,2},{3,4},{4,5},{5,8},{8,9},{9,10},{10,11},{5,6},{6,7}};
	vector<vector<int>> adj(n)  ;
	
	for (vector<int> e : edges) {
	    adj[e[0]].push_back(e[1]) ;
	    adj[e[1]].push_back(e[0]) ;
	}
	vector<int> dia = getDia(n , adj);
	for (int nodes : dia) {
	    cout << nodes  << " ";
	}
	cout << endl ;
	return 0 ;
}

```
