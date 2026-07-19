# DFU DSU 
-.https://codeforces.com/contest/570/my
```cpp
#include <bits/stdc++.h>
using namespace std;

#define ll long long 
typedef pair<ll, ll> pll;

const ll MAXN = 5e5 + 5;
ll subtree_sz[MAXN];
ll heavy[MAXN];
ll depth[MAXN];
ll cnt[MAXN]; // cnt[d] stores the 26-bit character mask for depth d
ll ans[MAXN];

vector<vector<ll>> adj;
vector<vector<pll>> queries; // queries[u] = {required_depth, query_index}
string s;

// Step 1: Compute subtree sizes and identify heavy children
void dfs_sz(ll u, ll par) {
    subtree_sz[u] = 1;
    ll mx_sz = -1;
    heavy[u] = -1; // Initialize heavy child as -1
    
    for (const ll &v : adj[u]) {
        if (v == par) continue;
        depth[v] = depth[u] + 1;
        dfs_sz(v, u);
        
        subtree_sz[u] += subtree_sz[v];
        if (subtree_sz[v] > mx_sz) {
            mx_sz = subtree_sz[v];
            heavy[u] = v;
        }
    }
}

// Helper function to add/remove a node and its entire subtree to/from the global cnt array
void add(ll u, ll par, ll val) {
    ll ch = s[u - 1] - 'a'; // Convert 1-indexed node to 0-indexed string character
    cnt[depth[u]] ^= (1LL << ch); // Flip the bit for odd/even tracking
    
    for (const ll &v : adj[u]) {
        if (v == par) continue;
        add(v, u, val);
    }
}

// Step 2: DSU on Tree main logic
void dfs_dsu(ll u, ll par, bool keep) {
    // 1. Run DFS on light children and don't keep their data
    for (const ll &v : adj[u]) {
        if (v == par || v == heavy[u]) continue;
        dfs_dsu(v, u, false);
    }
    
    // 2. Run DFS on the heavy child and keep its data
    if (heavy[u] != -1) {
        dfs_dsu(heavy[u], u, true);
    }
    
    // 3. Add the current node and its light subtrees to the maintained heavy child data
    ll ch = s[u - 1] - 'a';
    cnt[depth[u]] ^= (1LL << ch);
    
    for (const ll &v : adj[u]) {
        if (v == par || v == heavy[u]) continue;
        // Collect data from light subtrees manually
        // We temporarily pass 1 (or any placeholder) as it just toggles the bits
        add(v, u, 1); 
    }
    
    // 4. Answer all queries for the current node 'u'
    for (auto &[req_d, idx] : queries[u]) {
        // If the requested depth is out of bounds or empty, popcount is 0 <= 1 (True)
        ll mask = cnt[req_d];
        if (__builtin_popcountll(mask) <= 1) {
            ans[idx] = 1; // Palindrome is possible
        } else {
            ans[idx] = 0; // Palindrome is impossible
        }
    }
    
    // 5. Clean up if this node was a light child of its parent
    if (!keep) {
        // Calling add again acts as a perfect rollback because of the XOR property (A ^ A = 0)
        ll ch_del = s[u - 1] - 'a';
        cnt[depth[u]] ^= (1LL << ch_del);
        for (const ll &v : adj[u]) {
            if (v == par) continue;
            add(v, u, -1);
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    ll n, m;
    if (!(cin >> n >> m)) return 0;
    
    adj.resize(n + 1);
    queries.resize(n + 1);
    
    for (ll i = 2 ; i <= n ; i++) {
        ll p;  cin >> p;
        
        adj[p].push_back(i);
        adj[i].push_back(p);
    }
    
    cin >> s;
    
    for (ll j = 0; j < m; j++) {
        ll u, h;
        cin >> u >> h;
        queries[u].push_back({h, j});
    }
    
    // Run precomputations starting from root node 1 at depth 1
    depth[1] = 1 ;
    dfs_sz(1, -1) ;
    
    // Run the DSU processing
    dfs_dsu(1, -1, true);
    
    // Print results
    for (ll j = 0; j < m; j++) {
        if (ans[j]) cout << "Yes\n";
        else cout << "No\n";
    }
    
    return 0;
}
```
