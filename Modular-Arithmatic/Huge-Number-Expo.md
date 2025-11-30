# Huge-Number-Expo

- On top of mod-expo keep in mind we sometimes need to take the mod of expo as well !

### Exponent Reduction (Crucial!)
$\phi(M)$
- The exponent B must be reduced modulo {read it as phi} : Q(M) , where Q(M) is Euler's Totient function. This is based on Euler's Theorem.
- `const ll exp_mod = mod - 1 ;`

### Base Reduction :
- Normal mod expo for the base : (A.B) mod m = ((A  mod m) . (B mod m)) mod m

- Huge numbers :Handling Large Inputs (String Processing)
- For `a^b` where both are huge : for do : `a mod m `  && `b mod expo_mod` where expo_mod = mod-1 while converting strings to long long int


```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long

const ll mod = (ll)1e9 + 7 ;
const ll exp_mod = mod - 1 ; 
// The l : ie mod-2 for expo  totient func {power}

ll string_to_mod(string s , ll m) { // different for base and expo 
    ll res = 0LL ;
    for (char c: s) {
        res = (10LL * res + (c-'0'))% m ;
    }
    return res ;
}
ll mod_expo(ll base , ll expo) {
    ll res = 1LL ;
    
    while (expo > 0) {
        if (expo&1) res = (1LL * res * base ) % mod ;
        base = ( 1LL * base * base ) % mod ;
        expo >>= 1 ;
    }
    return res ;
}

int main() {
    ll t ;
    cin >> t ;
    
    while (t-- > 0) {
        string a , b ;
        cin >> a >> b ;
        ll num = string_to_mod(a, mod) ;
        ll p = string_to_mod(b , exp_mod) ;
        
        cout << mod_expo(num , p) << "\n" ;
        
    }
    
}

```
