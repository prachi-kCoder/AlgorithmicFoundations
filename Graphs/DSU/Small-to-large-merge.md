## Small-to-large-merge
- here : https://codeforces.com/problemset/problem/600/E
```
- SMALLER TO LARGE is by swapping the root `mp` to `childmap` reference exchange so that to ensure we make least possible insertions
- Even if swapped then also childmap is to be inserted do not forget {to merge the per smaller sized root now exchanged!}
- `WHY NLOGN ?` : as mp_sz = 5 will be exchanged by atleast with sz = 6 => merged sz = 11 , then it needs any node will be moved only if size is atleast sz + 1 ,
- {Movement of element is doubling the merged overall size } 2->5->11->23 ... so (LOGN)  for every node so TC = N(logN)
- we need to also handle leaf cases is mp[a[u]]++ and then comp with mp[a[u]] is imp in case its just the leaf node with no nbrs !
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long

const ll MAXN = (ll)1e5 + 5;
vector<vector<ll>> adj;
vector<ll> ans;

void dfs(ll u, ll par, vector<ll>& a, unordered_map<ll, ll>& mp, ll& mx, ll& sum) {
    mp[a[u]]++;
    if (mp[a[u]] > mx) {
        mx = mp[a[u]];
        sum = a[u];
    } else if (mp[a[u]] == mx) {
        sum += a[u];
    }

    for (ll v : adj[u]) {
        if (v == par) continue;
        unordered_map<ll, ll> child_mp;
        ll child_mx = 0, child_sum = 0;
        dfs(v, u, a, child_mp, child_mx, child_sum);

        if (child_mp.size() > mp.size()) {
            swap(mp, child_mp);
            swap(mx, child_mx);
            swap(sum, child_sum);
        }

        for (auto& [color, freq] : child_mp) {
            mp[color] += freq;
            if (mp[color] > mx) {
                mx = mp[color];
                sum = color;
            } else if (mp[color] == mx) {
                sum += color;
            }
        }
    }

    ans[u] = sum;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);

    ll n;
    cin >> n;

    vector<ll> a(n);
    for (ll& e : a) cin >> e;

    adj.resize(n);
    ans.resize(n, 0);

    for (ll i = 1; i < n; i++) {
        ll u, v;
        cin >> u >> v;
        u--, v--;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    unordered_map<ll, ll> mp;
    ll mx = 0, sum = 0;
    dfs(0, -1, a, mp, mx, sum);

    for (ll i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
    cout << endl;

    return 0;
}
```
