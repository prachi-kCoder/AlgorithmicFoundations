## Counting-Numbers
- CSES (DP - PROBLEM)
  
#### DIMENSIONS :
    - `Tight` : Ensures the digit used at every ith index does not crosses the limit
    - `leading_zero` : To take up number with smaller length than of the max_num given ,
        Eg :000123, the leading zeros are ignored in terms of adjacency.
        But for 1123, the 11 violates the rule — and your if (d == prev && !leading_zero) correctly skips it. 
    - 'Prev' : To keep track of prev_digit to resist repetition of digit in number formed .


```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) 
#define ll long long 
using namespace std;
ll dp[20][2][2][10] ;
ll helper(int i ,bool tight , const string& s, bool leading_zero ,int prev) {
    if(i >= s.length()) return 1LL ;
    if (prev != -1 && dp[i][tight][leading_zero][prev] != -1LL) {
        return dp[i][tight][leading_zero][prev] ;
    }
    ll c = 0LL ;
    int limit = (tight) ? s[i]-'0' : 9 ;
    
    for (int d = 0 ; d <= limit ; d++) {
        if (d == prev && !leading_zero) {
            // cout << "at prev :"  << prev << " & d :" << d << endl ;
            continue ;
        }
            
        c += helper(i+1 , tight&&(d==limit) , s , (leading_zero&&(d==0)) , d );
    }
    return dp[i][tight][leading_zero][prev] = c ;
}
ll count(ll num) {
    string s = to_string(num) ;
	memset(dp , -1LL , sizeof(dp)) ;
	return helper(0 , true , s ,true , -1 ) ;
}
int main() {
    FASTIO ;
	ll a , b ;
	
	cin >> a >> b ;
	
	ll v1 = count(a-1) ;
	ll v2 = count(b) ;

	cout << (v2 - v1) << endl ;
	return 0 ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*2*2*10) | N-> length of num {b} , binary states:(leading_zero, tight) , 0-9 {Prev digit} |
| 🧠 SPACE |   O(N*2*2*10)        | Dp table |

