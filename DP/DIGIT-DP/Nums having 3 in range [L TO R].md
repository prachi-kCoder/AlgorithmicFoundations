# DIGIT - DP 

### // How many numbers between L and R (inclusive) contain the digit '3' at least once?
```cpp
#include <bits/stdc++.h>
#include<cstring>
#define ll long long 
using namespace std;
ll dp[20][2][2][2]; 
ll count(int pos , bool tight, bool is_leading_zero, bool used3 , int n , const string& s ) {
    if (pos >= n) return used3 ? 1LL : 0LL ;
    
    if (dp[pos][tight][is_leading_zero][used3] != -1LL ) return dp[pos][tight][is_leading_zero][used3] ;
    
    ll ans = 0LL ;
    int limit = tight ? s[pos]-'0' : 9 ;
    
    for (int d = 0; d <= limit  ; d++ ){
        if (is_leading_zero && d == 0) {
            ans += count(pos + 1 , tight&&(d==limit) , true , false , n , s);
        }else {
            ans += count(pos + 1 , tight&&(d==limit) , false , used3 || (d== 3) , n , s);
        }
    }
    
    return dp[pos][tight][is_leading_zero][used3] = ans ;
}
ll solve(int  num) {
    if (num < 3) return  0 ;
    memset(dp, -1LL , sizeof(dp)) ;
    string s = to_string(num) ;
    
    return count(0 , true , true , false , s.length() ,s );
}
int main() {
	int l = 2 ;
	int r = 267 ;
	cout << solve(r) - solve(l-1) << endl ;
	
	return  0 ;
}
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  | O(n * 2 *2* 2)     | Explore upto n positions , Binary flags(0/1) : tight,is_leading_zero, used3 |
| 🧠 SPACE |   O(n * 2 *2 * 2)   |   DP - Table         |
