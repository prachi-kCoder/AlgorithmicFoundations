# HEAVY - LIGHT DECOMPOSITION
- Path queries and updates over trees
- If queries are to be made over a tree , then CREATE LINEAR seq of tree then give to SEGMENT TREE
- `HEAVY SEQUENCES ARE CONSECUTIVE `
- `2 nodes on diff seq are LIFTED till their heads are same! -> ie they come over the same path path which is consecutively saved in Segment Tree, so segtree given the sum rightly !`

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 

class SegTree {
    vector<ll> tree;
    int n;

    void build(int node, int start, int end, const vector<ll>& seq, const vector<ll>& val) {
        if (start == end) {
            tree[node] = val[seq[start]];
            return;
        }
        int mid = (start + end) / 2;
        build(2 * node + 1, start, mid, seq, val);
        build(2 * node + 2, mid + 1, end, seq, val);
        tree[node] = tree[2 * node + 1] + tree[2 * node + 2];
    }

    ll query(int node, int start, int end, int l, int r) {
        if (r < start || end < l) return 0;
        if (l <= start && end <= r) return tree[node];
        int mid = (start + end) / 2;
        return query(2 * node + 1, start, mid, l, r) + query(2 * node + 2, mid + 1, end, l, r);
    }

    void update(int node, int start, int end, int idx, ll new_val) {
        if (start == end) {
            tree[node] = new_val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(2 * node + 1, start, mid, idx, new_val);
        else update(2 * node + 2, mid + 1, end, idx, new_val);
        tree[node] = tree[2 * node + 1] + tree[2 * node + 2];
    }

public:
    SegTree(int n, const vector<ll>& seq, const vector<ll>& val) {
        this->n = n;
        tree.assign(4 * n, 0);
        build(0, 0, n - 1, seq, val);
    }
    ll query(int l, int r) { return query(0, 0, n - 1, l, r); }
    void update(int idx, ll val) { update(0, 0, n - 1, idx, val); }
};

vector<vector<ll>> adj;
vector<ll> parent, head, heavy, subtree_sz, depth, pos, val;
int cur_pos;

void dfs_sz(ll u, ll p, ll d) {
    subtree_sz[u] = 1;
    parent[u] = p;
    depth[u] = d;
    ll max_subtree = 0;
    for (ll v : adj[u]) {
        if (v == p) continue;
        dfs_sz(v, u, d + 1);
        subtree_sz[u] += subtree_sz[v];
        if (subtree_sz[v] > max_subtree) {
            max_subtree = subtree_sz[v];
            heavy[u] = v;
        }
    }
}

void dfs_hld(ll u, ll h) {
    head[u] = h;
    pos[u] = cur_pos++;
    if (heavy[u] != -1) dfs_hld(heavy[u], h);
    for (ll v : adj[u]) {
        if (v != parent[u] && v != heavy[u]) {
            dfs_hld(v, v);
        }
    }
}

ll queryPath(int u, int v, SegTree &st) {
    ll res = 0;
    while (head[u] != head[v]) {
        if (depth[head[u]] < depth[head[v]]) swap(u, v);
        res += st.query(pos[head[u]], pos[u]);
        u = parent[head[u]];
    }
    if (depth[u] < depth[v]) swap(u, v);
    res += st.query(pos[v], pos[u]);
    return res;
}

int main() {
    ios::sync_with_stdio(0); cin.tie(0);
    int n, q;
    if (!(cin >> n >> q)) return 0;

    adj.assign(n, {});
    val.resize(n);
    parent.assign(n, -1);
    head.assign(n, -1);
    heavy.assign(n, -1);
    depth.assign(n, 0);
    subtree_sz.assign(n, 0);
    pos.assign(n, 0);

    for (int i = 0; i < n; i++) cin >> val[i];
    for (int i = 0; i < n - 1; i++) {
        int u, v; cin >> u >> v;
        u--; v--;
        adj[u].push_back(v); adj[v].push_back(u);
    }

    dfs_sz(0, -1, 0);
    cur_pos = 0;
    dfs_hld(0, 0);

    vector<ll> seq(n);
    for (int i = 0; i < n; i++) seq[pos[i]] = i;

    SegTree st(n, seq, val);

    while (q--) {
        int t; cin >> t;
        if (t == 1) {
            int u; ll x;
            cin >> u >> x; u--;
            st.update(pos[u], x);
        } else {
            int u, v;
            cin >> u >> v; u--; v--;
            cout << queryPath(u, v, st) << "\n";
        }
    }
    return 0;
}
```
