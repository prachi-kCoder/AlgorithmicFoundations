## nCr

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
