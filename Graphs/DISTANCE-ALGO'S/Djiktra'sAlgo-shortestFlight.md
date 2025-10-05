# DJIKTRA'S ALGO WITH SHORTEST PATH
## WITH DISCOUNT COUPON
- Key track fo

```cpp
#include <bits/stdc++.h>

using namespace std;
#define ll long long 
struct info{
    ll cost ; int node ;
    bool coupon_used ;
    info(ll c , int node, bool used) : cost(c) , node(node) , coupon_used(used) {}
};
struct comp {
    bool operator()(info &i1 , info &i2) {
        return i1.cost > i2.cost ;
    }
};
int main() {
    int n , m ;
    cin >> n >> m ;
    vector<vector<pair<int,int>>> adj(n) ;
    for (int i = 0 ; i < m ; i++) {
        int a , b , c ;
        cin >> a >> b >> c ;
        a-- , b-- ;
        adj[a].push_back({b,c}) ;
    }
    if (n == 1) {
        cout << 0LL << endl ;
        return 0 ;
    }
    // 0 -> not used , 1->used
    vector<vector<ll>> dist(n , vector<ll>(2, LLONG_MAX)) ;
    
    // 0 -> n-1
    dist[0][0] = 0 ;

    // nbr with cost 
    priority_queue<info,vector<info>,comp> pq ;
    info i1(0LL , 0 , false) ;// coupon not used
    pq.push(i1);// 0 node with no cost & no coupon !

    while (!pq.empty()) {
        info curr = pq.top() ; pq.pop();
        ll cost = curr.cost ;
        ll u = curr.node ; bool coupon_used = curr.coupon_used ;
        if ( dist[u][coupon_used] != cost ) {
            continue ;// stale data 
        } 

        for (auto[v ,wt]: adj[u]) {
            if (!coupon_used) {

                if (dist[v][0] > dist[u][0] + wt) {
                    dist[v][0] = dist[u][0] + wt ;
                    info nbr_info(dist[v][0], v, false);
                    pq.push(nbr_info);
                }
                if (dist[v][1] > dist[u][0] + wt/2) {
                    dist[v][1] = dist[u][0] + wt/2 ;
                    info nbr_info(dist[v][1], v, true);
                    pq.push(nbr_info);
                }
            }else {

                if (dist[v][1] > dist[u][1] + wt ) {
                    dist[v][1] = dist[u][1] + wt  ;
                    info nbr_info(dist[v][1], v, true);
                    pq.push(nbr_info);
                }
            }
        }
    }

    cout << min(dist[n-1][0] , dist[n-1][1]) << endl ;

    return 0;
}
```
