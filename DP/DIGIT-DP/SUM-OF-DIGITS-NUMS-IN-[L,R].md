# Sum of digits of all numbers in a range [L, R]

- first: count of valid numbers in subtrees
- second: total digit sum contributed by those numbers

```cpp
#include <bits/stdc++.h>
#include<cstring>
#include<vector>
#define ll long long
#define pll pair<ll,ll>
using namespace std;
pll dp[20][2][2] ; 
// What is the sum of digits of all numbers between L and R (inclusive)?"
pll solve(int pos , bool is_leading_zero , bool tight , const string& s ) {
    if (pos >= s.length()) return {1LL, 0LL};
    
    if (dp[pos][is_leading_zero][tight].first != -1LL )  {
        return dp[pos][is_leading_zero][tight] ;
    }
    pll ans = {0LL, 0LL}; 
    int limit = tight ? s[pos]-'0' : 9 ;
    
    for (int d = 0 ; d <= limit ; d++ ) {
        if (tight && d == 0) {
            pll c = solve(pos + 1 , true , tight && d==limit , s  );
            ans.first += c.first ;
            ans.second += c.second ; 
            // here d = 0 so currDigit have no contribution in sum ;
        }else {
            pll c = solve(pos + 1 , false , (tight && d == limit), s );
            ans.first += c.first ;
            ans.second += c.second + c.first*d ;
        }
    }
    return dp[pos][is_leading_zero][tight] = ans ;
}
ll count(int N) { // digitSum upto N 
    if (N <= 0) return 0LL ;
    string s = to_string(N) ;
    
    for (int i = 0; i < 20 ; i++) {
        for (int j = 0; j <= 1 ; j++) {
            for (int k = 0; k <= 1 ; k++) {
               dp[i][j][k] = {-1LL, -1LL} ;
            }
        }
    }
    
    return solve(0 , true , true  , s ).second ;
}
int main() {
    int l = 20 ;
    int r = 4536;
    cout << count(r) - count(l-1) << endl ;

    return  0 ;
}

```
## 🔍 Complexity Analysis
|  METRIC    | COMPLEXICITY  |   WHY ? | 
|-------------|-----------------|---------------|
| ⏱ Time	| O(n · 2 · 2) | Each position n , Binary flags : tight , is_leading_zero |
|  💾 Space	| O(n · 2 · 2) | Dp table storing count , sum  | 
