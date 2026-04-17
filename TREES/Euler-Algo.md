- HERE : https://codeforces.com/contest/383/problem/C
- `flat` : Linear DS for the tree , `flat[i] = node ` , ie @ ith insertion time the node_num = node is present
- `in` , `out` : [gives the range of time_zone] , ie {start - end}  timezones for everynode
- `val[node]` -> orignal node :
- `a[node]` : Signed values of each node based on even or odd depth , with the reference of rootnode the updations were always consistent !
- `depth[node]` : Every node depth from root node {ie taken as standard for everynode}
```
- Confusion arised when lazy - prop for that whole subtree was performed!
- 1->2->3->4  here 2,4-> {signed values are -ve }
 so if updations happen then 2,4 are updated with -ve delta  that effective adds up into it , consider val[node2] is updated so its at odd depth from 1
then -val[2] was originally kept so updating -delta makes it even -val[2] - delta and is child node +val[3] - delta so effectively we are adding at node2, and subtracting from ndoe3 !
```

```cpp
#include <bits/stdc++.h> 
using namespace std;

#define ll long long

vector<vector<ll>> adj ;
vector<ll> a , in , out ;
ll timer;
vector<ll> flat ; 
vector<ll> depth ;

struct SegTree {
    ll n ;
    vector<ll> tree , lazy ;
    
    SegTree(const vector<ll>& a) {
        n = a.size();
        tree.resize(4*n , 0 );
        lazy.resize(4*n , 0);
        build(0 , n-1 , a , 0);
    }  
    
    void build(ll s , ll e , const vector<ll>& a , ll idx) {
        if (s == e) {
            tree[idx] = a[s];   // ✅ FIX: directly use arr value
            return ;
        }
        
        ll mid = (s + e) / 2 ;
        build(s , mid , a , 2*idx + 1) ;
        build(mid+1 , e , a , 2*idx + 2) ;
    }

    void push(ll idx) {
        if (lazy[idx] != 0) {
            lazy[2*idx+1] += lazy[idx];
            lazy[2*idx+2] += lazy[idx];
            lazy[idx] = 0;
        }
    }

    ll query(ll si , ll ei , ll pos , ll idx) {
        if (si == ei) {
            return tree[idx] + lazy[idx];
        }
        push(idx);
        ll mid = (si + ei) / 2;
        if (pos <= mid)
            return query(si , mid , pos , 2*idx + 1);
        else
            return query(mid+1 , ei , pos , 2*idx + 2);
    }

    void update(ll si , ll ei , ll ql , ll qr, ll idx , ll delta ) {
        if (ei < ql || si > qr) return;

        if (si >= ql && ei <= qr) {
            lazy[idx] += delta;
            return;
        }
        
        push(idx);
        ll mid = (si + ei) / 2;
        update(si , mid , ql , qr , 2*idx + 1 , delta);
        update(mid+1 , ei , ql , qr , 2*idx + 2 , delta);
    }
};

void dfs(ll u , ll par) {
    in[u] = timer;
    flat[timer] = u;
    timer++;
    
    for (ll v : adj[u]) {
        if (v == par) continue;
        depth[v] = depth[u] + 1;   // ✅ FIX: move depth here
        dfs(v , u);
    }
    
    out[u] = timer - 1;
}

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);

    ll n, q;
    cin >> n >> q;

    a.resize(n);
    for (ll &x : a) cin >> x;

    adj.resize(n);
    for (ll i = 0; i < n-1; i++) {  
        ll u , v;
        cin >> u >> v;
        u-- , v--;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    in.resize(n);
    out.resize(n);
    flat.resize(n);          
    depth.resize(n, 0);

    timer = 0;
    dfs(0 , -1);

    vector<ll> arr(n);
    for (ll i = 0 ; i < n ; i++ ) {
        ll node = flat[i];
        
        if (depth[node] % 2 == 0)
            arr[i] = a[node];
        else
            arr[i] = -a[node];
    }

    SegTree t(arr);

    while (q--) {
        int type;
        cin >> type;
        
        if (type == 1) {
            ll x , val;
            cin >> x >> val;
            x--;

            ll delta = (depth[x] % 2 == 0 ? val : -val);  // ✅ FIX

            t.update(0 , n-1 , in[x] , out[x] , 0 , delta);
        } 
        else {
            ll x;
            cin >> x;
            x--;

            ll res = t.query(0 , n-1 , in[x] , 0);   // ✅ FIX

            if (depth[x] % 2 == 0)                   // ✅ FIX
                cout << res << '\n';
            else
                cout << -res << '\n';
        }
    }

    return 0;
}
```
