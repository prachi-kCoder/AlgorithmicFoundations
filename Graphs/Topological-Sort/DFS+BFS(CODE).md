# Topological-Sort
### BOTH DFS + BFS APPROACHES 
```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
#include <bits/stdc++.h>
using namespace std ;
vector<int> adj[10] ;
void helper(int node,  int n, bitset<10>& vis , vector<int>& topoOrder) {
    vis.set(node) ;
    // First visit nbr
    for (int nbr : adj[node]) {
        if (!vis.test(nbr)) {
            helper(nbr , n , vis, topoOrder) ;
        }
    }
    topoOrder.push_back(node) ;
}
void DFStopo(int n ) {
    bitset<10> vis(0) ;// at max 10 nodes
    vector<int> topoOrder ;
    for (int i = 0; i <n ; i++) {
        if (!vis.test(i)) {
            helper(i, n, vis, topoOrder) ;
        }
    }
    for (int i = topoOrder.size()-1 ; i>= 0 ;i--) {
        cout << topoOrder[i] << " " ;
    }
    cout << endl ;
}
// BFS topo
void BFStopo(int n , vector<pair<int,int>>& edges) {
    int inDeg[n] = {0} ;
    for (auto e : edges) {
        inDeg[e.second]++ ;
    }
    queue<int> q ;
    for (int i = 0; i < n ; i++) {
        if (inDeg[i]== 0) q.push(i);
    }
    while (!q.empty()) {
        int c = q.front() ; q.pop() ;
        cout << c <<" " ;
        for (int nbr : adj[c]) {
            inDeg[nbr]--;
            if (inDeg[nbr] == 0) {
                q.push(nbr) ;
            }
        }
    }
    cout << '\n' ;
}
int main() {
    // n< 10, DAG
    vector<pair<int,int>> edges = {{5,0},{4,0},{4,1},{5,2},{2,3},{3,1}};
    int n = 6; // [0,5]
    for (auto e: edges) {
        adj[e.first].push_back(e.second);
    }
    // topological order
    BFStopo(n,edges) ;
    DFStopo(n) ;
    
    return 0;
}
```

# 📊 Topological Sort Complexity Comparison
| Aspect	|DFS-Based Topo Sort	|BFS-Based Topo Sort (Kahn’s Algorithm)|
|-----------|-----------------------|------------------------------------|
| TIME     |  O(V + E)       |  O(V + E) |
| SPACE     |  O(V) -> vis , topoOrder vector/stack | O(V) inDeg , queue |
|Approach Type|	Post-order DFS traversal| Level-order BFS traversal |
| Which one's better ? | BFS is often preferred in scheduling-type problems for early detection of cycles . | DFS is elegant and stack-friendly, ideal when recursion depth is manageable.|
|        |     Cycle Detection if count of processed nodes < N  |  Sepater function to detect cycle 1st |
