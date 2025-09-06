# FINDING ARTICULATION POINTS IN GRAPH BY TARJAN'S ALGORITHM

# TARJAN'S ALGO
- Maintain low , tin, bool , is_arti
- **low[v] >= tin[u]** that means the node u is articulation because the nbr(v) if can't be vis at a low time ie  it is visited via the node u , and as soon as u node is removed the node v couldn't be visited result in the graph being split in disconneted parts
- Do check the node u is not 1st node of componect ie par != -1
- Because first node of graph comp is to be handle by checking whether it has unvisited children > 1 , then if u node (1st node) if removed then graph surely splits
- Do not forget to use is_arti / set<int> point  for only unique entries as multiple nbr of u can conclufe for u to be articulation pts hence to avoid duplication , get uniq articulation points marked & at the end print them up!
- & From already visited nbr we just take {not != par} tin[v]
  
 ```cpp
  #include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
int timer = 0 ;
void dfs(int node , int par , vector<bool>& vis, vector<int>& low , vector<int>& tin, vector<bool>& is_arti) {
    vis[node] = true ;
    low[node] = tin[node] = timer ;
    timer++ ;
    
    int children = 0 ;
    for (int v : adj[node]) {
        if (!vis[v]) {
            children++ ;
            dfs(v , node , vis , low, tin, is_arti) ;
            low[node] = min(low[node] , low[v]); 
            
            if (low[v] >= tin[node] && par != -1) {
                is_arti[node] = true;
            }
            
        }else if( v != par) {
            low[node] = min(tin[v], low[node]);
        }
    }
    if (par == -1 && children > 1) {
        is_arti[node] = true;
    }
}
void arti(int n) {
    vector<int> tin(n);
    vector<int> low(n);
    vector<bool> vis(n);
    vector<bool> is_arti(n,false) ;
    for (int i = 0; i < n ; i++) {
        if (!vis[i]) {
            dfs(i , -1 , vis , low , tin, is_arti) ;
        }
    }
    for (int i = 0; i < n; i++) {
        if (is_arti[i]){
            cout << (i+1) << " ";
        }
        cout << endl ;
    }
}
int main() {
    // undirected
    vector<vector<int>> edges = {{1,2},{2,3},{1,3},{3,4},{4,8},{4,5},{8,9},{9,10},{10,8},{5,7},{7,6},{6,5}};
    int n = 10 ;
    adj.resize(10) ;
    for (vector<int> e : edges) {
        int u = e[0] ; int v = e[1] ;
        u-- , v-- ;// 0 based
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    arti(n ) ;
    return 0 ;
}

}
``` 

