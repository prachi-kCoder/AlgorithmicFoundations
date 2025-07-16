# Kosaraju Algorithm
```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
#include <bits/stdc++.h>
using namespace std ;
void dfs(int u , stack<int>& stk , vector<bool>& vis , vector<int> adj[])  {
    vis[u] = true ;
    for (int v : adj[u]) {
        if (!vis[v]) {
            dfs(v , stk, vis , adj) ;
        }
    }
    stk.push(u) ;
}
void dfs2(int u , vector<bool>& vis , vector<int> adj[] ) {
    vis[u] = true ;
    for (int v : adj[u]) {
        if (!vis[v]) {
            dfs2(v , vis , adj) ;
        }
    }
}
int main() {
    vector<pair<int,int>> edges = {{0,1},{1,2},{2,0},{2,3},{3,4},{4,5},{5,6},{6,4},{4,7},{6,7}} ;
    int n = 8 ;
    vector<int> adj[n] ;//[0-7]
    for (auto e :edges) {
        adj[e.first].push_back(e.second) ;
    }
    vector<bool> vis(n)  ;
    stack<int> stk ;
    for (int i = 0; i < n ; i++) {
        if (!vis[i]) {
            dfs(i , stk , vis, adj) ;
        }
    }
    vector<int> adjRev[n] ;
    for (int i = 0; i < n ; i++) {
        vis[i] = false ;
        for (int nbr : adj[i]) {
            adjRev[nbr].push_back(i) ;
        }
    }
    int scc = 0 ;
    while (!stk.empty()){
        int node = stk.top();
        stk.pop();
        if (!vis[node]) {
            scc++ ;
            dfs2(node , vis,adjRev);
        }
    }
    cout << "scc :" << scc << endl ;
    
    return 0;
}
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(V+E)       | Making Adj O(V+E) , dfs O(V+E) , RevADJ O(V+E) , dfs2(V+E)   |
| 🧠 SPACE |  O(V+E)       | adj, revAdj : O(V+E) , O(V) , recursion stack , vis , stack (finishTime order) |
