# LCM OF A SET OF NUMBERS 

-> nums = {3,6,7,8,10,12}
-> LCM on iteration from LHS->RHS LCN = P[i] / gcd
-> set of values {threshold is used in case Bsearch applies over answer} / to avoid integer overflow ! 

```
LCM_new = lcm(LCM_old , val / g ) , where LCM_old = LCM(all values considered ) , g= GCD(lcm_old , new_ele)
so LCM_new = (LCM_old * new_val )/ g 
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 

ll gcd(ll a , ll b) {
    if (b == 0) return a ;
    return gcd(b ,a%b) ;
}
int main() {
    vector<ll> mul = { 2,13,26,24,18 } ;
    // formula :-  L = lcm( L , new_val / g ) where g -> GCD(L , new_val)
    ll lcm = 1LL ;
    ll threshold = 1000 ;
    bool invalid = false ;
    // if a threshold is given to check if lcm < threshold
    
    for (const ll& val : mul) {
        ll g = gcd( lcm , val ) ;    
        if ( lcm > threshold / (val / g) ) {
            invalid = true ;
            break ;
        }
        lcm = (1LL * lcm * val ) / g  ;
    }
    
    if (invalid) {
        cout << "Thresold reached!" << endl ;   
    } else {
        cout << lcm << endl ;
    }
    
    return 0 ;
}

```
