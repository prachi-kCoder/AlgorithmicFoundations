## No-Carry-Addition

- For any number n :
- If we want to split it as addition of multiple nums following the constraits over the digitsum of n then applied:
- Such that n = a + b + c + d + ....   &  digit_sum(n) = digit_sum(a) + digit_sum(b) + digit_sum(c) + digit_sum(d) + ...
  
```
Property :
To keep the digit_sum(n) = digit_sum(a) + digit_sum(b) + digit_sum(c) + digit_sum(d) + ...
This equality holds if and only if the addition $a+b+c=n$ is performed without any carries in base 10.
, so all ones,  tens , hundreds ... all places should independently be contributing 
```

Proof :
`digit_sum(a) + digit_sum(b) + digit_sum(c) = digit_sum(n) + 9.c  , where c = carry`
Contribution to summands’ digit sum = 10𝑐+𝑑.  {Sum of digits at any place if c = 2 then 20 + d {d original digit at the pos}
Contribution to result’s digit sum = 𝑑+𝑐.  {In N the same place will be occpied by the original d & c from prev positions }
Difference = (10𝑐+𝑑)−(𝑑+𝑐)= 9𝑐.
### d_sum(a) + d_sum(b) + d_sum(c) .... = d_sum(N) + 9*c
So to make LHS = RHS  c = 0  that allows us to independently handle the possitions to get the ways of getting any digit in N at its position and taking all arrangements of ways of getting respective digit at a place !

- UNDERSTAND WITH THIS QUES IN WHICH WE NEED THE ALL POSSIBLE TRIPLETS SO THAT `A+B+C = N` & `D_sum(A) + D_sum(B) + D_sum(C) = D_sum(N) `

- For this here keep in mind since DigiSum constraint is to be followed then
- As per general rule : `D_Sum(a) + D_sum(b) + D_sum(c) = D_Sum(n) + 9*c` here c must be zero ie at every place we should not get any carry
- Hence take every digit position independently without as no carry will be forwarded
- Now to make a+b+c = N then at every position : the digit of N should be made by all possible ways
- Ie if N = 1341
- Ones place : 1 should be made {0,0,1} or {1,0,0} or {0,1,0} there are the digits are ones place in a,b,c
- Tens palce 4 should be made ie {0,0,4} {0,1,3} ... similarly the Exact digit in N should be formed by a,b,c collectively without no intervention of carries forwarded !

 - After getting the ways of getting the digits at respective places :Take the all arrangement of possible ways of forming that D0,D1,D2.. in N 


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
    ios_base::sync_with_stdio(false);
	cin.tie(nullptr);
	vector<ll> ways(10 , 0LL) ;
	for (ll i = 0 ; i <= 9 ; i++) {
        for (ll j = 0 ; j <= 9 ; j++) {
            if (i + j >= 10) break ;
            for (ll k =  0 ; k <= 9 ; k++) {
                if (i + j + k < 10) {
                    ways[i+j+k]++;
                }
            }
        }
    }
    
    ll t ;
    cin >> t ;
    while (t-- > 0) {
        string n ;
        cin >> n ;
        ll ans = 1LL ;
        for (char c :n) {
            ans *= ways[c-'0'] ;
        }
        
        cout << ans << endl ;
    }
    return 0;   
}
```

# TC = 𝑂(len(𝑁)+10^3)
