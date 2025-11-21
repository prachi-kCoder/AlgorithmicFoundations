# Binary-Lifting-Get-LCA.md
```
- 2 PHASES
### LEVELLING :
- Level them: First lift the deeper node up until both are at the same depth.
### LIFT TOGETHER
fOR [J = log-1 to 0 ]
- If up[u][j] != up[v][j], lift both up to those ancestors.
- If they are equal, you do nothing at that level and continue checking smaller jumps.
because their may be smaller jumps possible as from LCA & onwards they both will be having same ancestor ,
but we need the lowest possible ! ie the LCA !
 so continue in loop until j = 0 is check if until the direct par say its equal so no further lifting !

## Final step:
 After the loop, both u and v are just below the LCA. So the LCA is up[u][0].
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long

const ll LOG = 19;
const ll MAXN = 2e5+5;

vector<vector<ll>> adj;
ll up[MAXN][LOG];
ll depth[MAXN];

void dfs(ll u , ll par) {
    up[u][0] = par ;//direct
    depth[u] = (par == -1 ? 0 : depth[par] + 1) ;
    
    for (int v : adj[u]) {
        if (v != par) dfs(v , u) ;// go deep 
    }
}
void preprocess(int n) {
    for (ll j = 1 ; j < LOG ; j++) {
        for (ll i = 0; i < n ; i++) {
            if (up[i][j-1] != -1) {
                up[i][j] = up[up[i][j-1]][j-1] ;// split 2^j jump in 2 jumps
            } else {
                up[i][j] = -1 ;
            }
        }
    }
}
ll get_lca(ll u , ll v) {
    if (depth[u] < depth[v]) swap(u,v);

    // Lift u up to same depth as v
    for (ll j = LOG-1 ; j >= 0 ; j--) {
        if (up[u][j] != -1 && depth[u] - (1<<j) >= depth[v]) {
            u = up[u][j];
        }
    }

    if (u == v) return u;

    // Lift both until their parents match
    for (ll j = LOG-1 ; j >= 0 ; j--) {
        if (up[u][j] != up[v][j]) {
            u = up[u][j];
            v = up[v][j];
        }
    }
    return up[u][0];
}
int main() {
	ll n , q;
	cin >> n >> q ;
	adj.resize(n);
	
	
	for (ll i = 0; i < n-1 ; i++) {
	    ll a , b ;
	    cin >> a >> b ;
	    a-- , b-- ;
	    adj[a].push_back(b);
	    adj[b].push_back(a);
	}
	memset(up , -1 , sizeof(up)) ;
	memset(depth , 0 , sizeof(depth)) ;
	dfs(0 , -1) ;
	preprocess(n);
	
    for (ll j = 0; j < q ; j++) {
        ll u , v ;
        cin >> u >> v ; 
        u-- ,v-- ;
        cout << get_lca(u,v)+1 << endl ;
    }

	return 0 ;

}

```

## TC :
- O(NLOGN + QlogN) = For all N nodes binary lifting of logN and for all Q queries again to get LCA logN is applied
## SC :
O(NLOGN)
