## Balanced-Distribution (Convex Optimisation)

- Here :https://leetcode.com/problems/minimum-sum-of-squared-difference/description/
- Convex objective function : sum of (diff^2) since the second derivation is always +ve => GREEDY IS THE BEST STRATEGY THEN !
- Intuition is to make optimally do the reduction in differences of all values in i indices
```
- Take differences : diff[i]
- Descending sort to lower high abs difference first!->Greedy
- Then reduce it until it becomes equals to the next value with the available moves
- Diff = {10 , 9 , 5, 1} -> {9 , 9 , 5 , 1 } -> {5, 5, 5, 1} -> {1,1,1,1}
This kind of reduction is preferred : Keep track of available cnt , if less that neede then reduct some of the prev ones by tht rem moves and just get the sum of sqres of the values as answer
```

- This is for exactly k1 + k2 moves to be applied
- In case atmost K1+K2 moves then -> just modify the in the condtion in case K1+K2 >= sum of abs diff in value {max needed} then return 0 , no matter odd or even rem , we just leave the reat moves unused.

```cpp
#include <bits/stdc++.h>
using namespace std;
#define IO ios_base::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define ll long long

int main() {

    IO;
    ll n , k1 , k2 ;
    if (!(cin>> n >> k1 >> k2)) return 0LL;
    
    vector<ll> a(n) , b(n) ;
    for (ll &x :a) cin>> x ;
    for (ll &y :b) cin>> y ;
    vector<ll> v(n) ;
    ll comp_D = 0LL;
    for (ll i = 0;i< n ; i++) {
        v[i] = abs(a[i] - b[i]) ;
        comp_D += v[i] ;
    }
    ll move = k1 + k2 ;
    if (comp_D <= move) {
        ll rest = move - comp_D ;
        cout << (rest%2 ? 1 : 0) << "\n" ;
        return 0 ;
    }
    
    if (move == 0) {
        ll ans = 0LL;
        for (ll x : v) ans += 1LL*x*x ;
        cout << ans << "\n" ;
        return 0;
        
    }
    sort(v.rbegin() , v.rend()) ;
    ll ans = 0LL;
    for (ll i = 0; i < n ; i++) {
        if (v[i] == 0) break;
        ll cnt = i+1 ;
        ll next_val = (i < n-1 ? v[i+1] : 0LL) ;
        ll red_ht = v[i] - next_val ;
        ll moves_needed =  1LL * cnt * red_ht ;
        if (move >= moves_needed) {
            move -= moves_needed ;
        }else {
            ll right_rem = 0;
            for (ll j = i + 1; j < n; j++) {
                right_rem += v[j] * v[j]; // accumulate
            }
            ans += right_rem;
            
            ll base_val = move / cnt ;
            ll c1 = move % cnt ;
            ll c2 = cnt - c1 ;
            
            ll more_red = v[i] - (base_val + 1);
            ll less_red = v[i] - base_val ;
            
            ans += 1LL * c1 * more_red * more_red + 1LL * c2 * less_red * less_red;
            cout << ans << "\n" ;
            return 0 ;
        }
    }
    
    for (ll x : v) ans += x * x; // fallback, though typically covered above
    cout << ans << '\n';
    return  0 ;

}

```
