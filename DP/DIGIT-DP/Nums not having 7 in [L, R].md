
# How many numbers between L and R (inclusive) do NOT contain the digit '7'? 

```cpp
#include <bits/stdc++.h>
#include<cstring>
#include<vector>
#define ll long long 
using namespace std;
ll dp[20][2][2][2]; 
ll solve(int pos , bool tight , bool is_leading_zero , bool used7, const string& s , int n) {
    if (pos >= n) return !used7 ? 1LL : 0LL;
    if (dp[pos][tight][is_leading_zero][used7] != -1LL) return dp[pos][tight][is_leading_zero][used7] ;
    int limit = tight ? s[pos] - '0' : 9 ;
    
    ll ans = 0LL ;
    for (int d = 0 ; d <= limit ; d++) {
        if (is_leading_zero && d == 0) {
            ans += solve(pos+1 , false , true , false , s , n) ;
        }else {
            ans += solve(pos+1 , tight&&(d==limit) , is_leading_zero && (d == 0) , used7 || d== 7 , s , n) ; 
        }
    }
    return dp[pos][tight][is_leading_zero][used7] = ans ;
}
ll count(int num){
    if (num < 7) return num ;
    memset(dp , -1LL, sizeof(dp));
    string  s = to_string(num) ;
    return solve(0 , true , true , false , s , s.length()) ;
}
int main() {
	int l = 3 ;
	int r = 50 ;
	cout << count(r) - count(l-1) << endl ;
	return  0 ;
}

```
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  | O(n * 2 *2* 2)     | Explore upto n positions , Binary flags(0/1) : tight,is_leading_zero, used3 |
| 🧠 SPACE |   O(n * 2 *2 * 2)   |   DP - Table         |
