## nCr
- BEST WAY TO GET FACT WITHOUT APPLY ANY MOD - ARITHMETIC , IF not more that INF is 10^18 is the limit otherwise the mod fact,inv fact is right !
  
```cpp
ll C[62][62];
    const ll INF = 2e18; // Slightly more than max possible n

    void precompute() {
        for (int i = 0; i <= 61; i++) {
            C[i][0] = 1LL;
            for (int j = 1; j <= i; j++) {
                // Saturated addition to prevent overflow
                if (C[i-1][j-1] >= INF || C[i-1][j] >= INF || (C[i-1][j-1] + C[i-1][j]) >= INF)
                    C[i][j] = INF;
                else
                    C[i][j] = C[i-1][j-1] + C[i-1][j];
            }
        }
    }
```
`n! /((n-r)!*(r!))`

- fact , invfact are necessary as to compute the div {No division operator in mod-arithmetic} so we multiply with invFact of the deno terms
- invfact[n] = mod_inv(fact[n])
### RECURRENCE RELATIONS USED :
- FACT : fact[n] = n*(fact[n-1]) 
- INV-FACT : invfact[n] = (n+1)*(invfact[n+1])

### MOD-EXPO :
- Done efficiently such that integer overflow never happens so we solve :
- a^x -> Split in (a^2)^(x/2) ;
- On each level of squaring do take MOD . Take care of odd powers as well!
```cpp
#define ll long long
class Solution {
  public:
  const int MOD = (int)1e9 + 7 ;
  vector<ll> fact ,invfact ;
    ll mod_expo(ll base , ll expo) {
        ll res = 1;
        while (expo > 0) {
            if (expo & 1) res = (res * base) % MOD;
            base = (base * base) % MOD;
            expo >>= 1;
        }
        return res;
    }
    ll mod_inv(ll base) {
        return mod_expo(base, MOD - 2);
    }
    void init(int n) {
        fact.resize(n + 1);
        invfact.resize(n + 1);
        fact[0] = 1;
        for (int i = 1; i <= n; ++i)
            fact[i] = (fact[i - 1] * i) % MOD;
            
        invfact[n] = mod_inv(fact[n]);
        
        for (int i = n - 1; i >= 0; --i)
            invfact[i] = (invfact[i + 1] * (i + 1)) % MOD;
    }
    int nCr(int n, int r) {
        if (r < 0 || r > n) return 0 ;
        
        init(n) ;
        return (((1LL*fact[n]*invfact[n-r])%MOD)*invfact[r])%MOD ;
    }
};
```


# METHOD 2: Iterative Fraction Method
- BEST in case nCr is need once or Twice so small and easy code 
```
nCr = n! / (r! * (n-r)!) => {n *..* (n-r+1) * (n-r)! } / r! * (n-r)! => then simplified => {1LL * n * ( n-r+1 ) / r! }
So simply get : n*(n-1)*(n-2)*...*(n-r+1) / r!  it works fine
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define IO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
#define ll long long

const ll mod = (ll)998244353 ;

ll mod_expo(ll base , ll expo) {
    ll res = 1LL ;
    while (expo > 0) {
        if (expo&1) res = (1LL * res * base ) % mod ;
        base = (1LL * base * base ) % mod ;
        expo >>= 1 ;
    }
    return res ;
}
ll mod_inv(ll x ) {
    return mod_expo(x , mod-2) ;
}
ll nCr(ll n , ll R) {
    ll res = 1LL ;
    
    for (ll r = 1 ; r <= R ; r++) {
        res = (1LL * res * (n-r+1))% mod ;
        res = (1LL * res * mod_inv(r)) % mod ;
    }
    return res ;
}
int main() {
    ll n , r; 
    cin >> n >> r ;
    cout << nCr(n , r) << endl ;
    return 0;
    
}

```
