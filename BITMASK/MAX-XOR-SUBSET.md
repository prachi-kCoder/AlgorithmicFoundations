- Use Gaussian Elimiation : Vector space (GE(2))
- Get the basis array
- Using the basis array- > Get the max_xor of the linearly indepently vectors taking charge of ith positions of B[i]  {MSB - > LSB} ie 64 bits!


  
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
const ll MAX_BITS = 32;
vector<ll> make_basis(vector<ll>& a) {
    vector<ll> basis(MAX_BITS , 0) ;
    
    for (ll x : a) {
        
        for (ll i = MAX_BITS - 1 ; i >= 0 ; i--) {
            if (!((x >> i)&1)) {
                continue ;
            }
            if (basis[i] == 0) {
                basis[i] = x ;
                // Case 1: New Pivot.
                // The i-th bit is set in x, and there's no existing generator.
                break ;
            }else {
                // Case 2: Elimination (The Gaussian step).
                // Use the existing pivot basis[i] to eliminate the i-th bit in x.
                x ^= basis[i] ; 
            }
        }
    }
    return basis ;
}
ll mx_subset_xor(vector<ll>& a){
    vector<ll> basis = make_basis(a) ;
    
    ll res = 0LL ;
    for (ll p = MAX_BITS-1 ; p >= 0 ; p--) {
        res = max(res , (res^basis[p])) ;
    }
    return res ;
}
int main() {
    ll n ;
    cin >> n ;
    vector<ll> a(n) ;
    for (ll i = 0 ; i < n ; i++) {
        cin >> a[i] ;
    }
    cout << mx_subset_xor(a) << "\n" ;
    return 0 ;
}

```

###### TC : O(64 * N) -> BASIS ARRAY FORMATION , O(64) for counting max_xor from basis array
- SC O(64)
