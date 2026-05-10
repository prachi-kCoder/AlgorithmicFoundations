# ReRooting-DP

- 2 imporatant variation i saw in :
### TREE DIAMETER 2 {Sum of distance of each node to every other nodes were necessary}
```cpp
POSTORDER
void postOrder(int u , int par ) {
    subtree_sz[u] += 1 ;
    for(ll v : adj[u]) {
       if (v == par) continue ;
         postOrder(v , u) ;
        subtree_sz[u] += subtree_sz[v] ; 
        dp[u] += dp[v] + subtree_sz[v] ; 
    }
}
void preOrder(int u , int par) {
    for (ll v : adj[u]) {
       if (v == par) continue ;
        dp[v] = dp[u] - subtree_sz[v] + (N-subtree_sz[v]) ;
        preOrder(v , u) ; 
     }
}
```

### Capital for Treeland :
- // get weight graph to  differentiate between directions : but here we are not always starting from 0 to reach any node
- so simpling counting wts is enough, as contigously moving !
```cpp
void postOrder(int u , int par) {

    for (auto &[v,wt] : adj[u]) {
         if (v == par) continue ;
         dp[0] += wt ; // not of inverses made in subtree of root 0 
         postOrder(v , u) ;
     }
 }
void preOrder(int u , int par) {

      for (auto &[v , wt] : adj[u)) {
          if (v == par) continue ;
          if (wt == 0) {// same dir 
              dp[v] = dp[u] + 1 ;
          } else {
              dp[v] = dp[u] - 1 ;
          }
          preOrder(v , u);
      }
}
```
  
