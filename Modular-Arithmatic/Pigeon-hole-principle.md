# Pigeon-hole-principle
```
If you have more numbers than boxes (𝑛>𝑚), then at least two numbers must fall into the same box. That means:
      𝑎𝑝≡𝑎𝑞(mod𝑚),𝑝≠𝑞

That will surely happen !
```
- One of the applications : https://codeforces.com/problemset/problem/1305/C
- Here you need to get the prod of abs diffence b/t all pairs ai,aj of array a
- But keep in mind if n>m  what is conveys : If more elements (n > m) then the mod value of any 2 values will surely overlap so their abs diff = 0 then the prod = 0

```cpp
#include <bits/stdc++.h>
// #include <ext/pb_ds/assoc_container.hpp>
// #include <ext/pb_ds/tree_policy.hpp>
using namespace std;
// using namespace __gnu_pbds;
#define IO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
#define ll long long
#define pll pair<ll,ll>
#define F first
#define S second
const ll mod = (ll)1e9 + 7 ;
// #define Oset tree<int, null_type, less<int>, rb_tree_tag, tree_order_statistics_node_update>
int main() {
    // ll t ;
    // cin >> t ;
    // while (t-- > 0) {
        ll n , m;
        cin >> n >> m;
        vector<ll> a(n) ;
        for (ll &x : a) cin >> x ;
        if (n > m) {
            cout << 0LL << endl ;
            return 0 ;
        }
        
        ll prod = 1LL ;
        for (ll i = 0; i < n ; i++) {
            for (ll j = i+1 ; j < n  ; j++) {
                prod = (1LL * prod * abs(a[i] - a[j])) % m ;
            }
            if (prod == 0 ) break;
        }
        cout << prod << endl ;
        
    // }
    
    return 0;
    
}

```
