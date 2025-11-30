# Last-Digit-Huge-Num-Expo
####  Finding the Last Digit mod 10
1) The Base Modulo 10: mod 10 :
- Last digit of a^b depends on last digit of a ie base : 3^5 = 123^5 , 7^2 = 127^7 so .. focus is the last digit of base a only so reduce the big base number to get the last digit only 
  
3) EXPO modulo 4 :
  For any power the expo cycle is at max of len = 4
Eg |  Base |   Power  |  Cycle Len   |
   |---------|------------|-------------|
   |  0 , 1 | 0 ,1,2,3,.. |     1       |
   |  2   | 2,4,8,6,.. repeat | 4  |  
   |  3   | 3,9,7,1,.. repeat | 4  |  
   |  4   | 4,6,4,6,.. repeat | 2  |
   .. similar for all 

- Now the last crucial check is :
- If `b = 4`, then `b mod{4} = 0` . However, `a^4` is the end of the cycle, not the beginning (which would be a^0 = 1 ).

- So the Totient Theorem says :
- Case 1: If b mod 4 != 0 : then `b' = b mod 4`
- Case 2: If b mod 4 = 0  => b' = 4    (if b > 4 & b mod 4 comes out to 0 )

Eg : If 7^20 = 7^4  but mod 4 given expo = 0 which is 7^0 = 1 ie incorrect !

```cpp
#include <bits/stdc++.h>
using namespace std;
#define IO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
#define ll long long
#define pll pair<ll,ll>
#define F first
#define S second
const ll mod = (ll)1e9 + 7 ;

ll get_mod_ll(const string& a , ll m) {
    ll res = 0LL ;
    for (char c : a) {
        res = (10LL * res + (c-'0') ) % m ;
    }
    return res ;
}
ll mod_expo(ll base , ll expo , ll m) {
    ll res = 1LL ;
    while (expo > 0) {
        if (expo&1) res = (1LL * res * base ) % m ;
        base = (1LL * base * base ) % m ;
        expo >>= 1  ;
    }
    return res ;
}
int main() {
    ll t ;
    cin >> t ;
    while (t-- > 0) {
        string a , b ;
        cin >> a >> b ;
        
        // get last digit of a^b where a,b are very big nos ;
        ll base = get_mod_ll(a , 10 );
        ll expo = get_mod_ll(b , 4);
        
        bool is_big_b = (b.length() > 1 || b[0] > '3') ;
        if (expo == 0 && is_big_b) {
            expo = 4 ;
        }
        
        ll last = mod_expo(base , expo, 10) ;
        
        cout << last << "\n" ;
    }
    return 0;
    
}

```
