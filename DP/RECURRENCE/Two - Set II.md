## Two - Set II
## POINTS TO KEEP IN MIND :
- ✅ Why Decreasing j in DP Ensures Each Number Is Used at Most Once :
   ```cpp
    for (int j = target; j >= num; --j)
   ```
    - This is to ensure while a sum value j we use the num only once as larger values of j are made before , rather than j = num upto j <= target , because the updated count of ways to form smaller sum j , can be used to form larger values of j (target) which should not happen as 1 num is appearing only once and should be used atmost once .
    - Larger values of j can't contribut to the formation of smaller values of j hence , they 're formed with the values of count cal by the num processed in prev iterations .
- Take **half** as same sum can be made by taking either the first set or the second set of nums , but its actully the same split of numbers
- Eg : nums = {1,2,3,4} then for sum = 10  Picking up {1,4} or {2,3} means the same split hence it should be counted as 1 .
- 
```cpp
#include <bits/stdc++.h>
#define ll long long
const int MOD = (int)1e9 + 7 ;
using namespace std;

int main() {
    int n ;
    cin >> n ;
    int totalSum = n*(n+1)/2 ;
    if (totalSum%2) {
        cout << 0LL<< endl ;
        return 0 ;
     }
    int target = totalSum/2 ;
    vector<ll> dp(target+1 , 0LL) ;
    dp[0] = 1LL ;
    for (int num = 1 ; num <= n ; num++) {
        for (int j = target ; j >= num ; j--) {
            dp[j] = (dp[j] + dp[j-num])%MOD ;
        }
    }
    cout << (dp[target] * 1LL * ((MOD+1)/2))%MOD << endl ;
    return  0 ;
 }

```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  | O(n*(n*(n+1)/4)) = O(n^3)     | n nums, tried for making all target values >= num   |
| 🧠 SPACE |    O(n*(n+1)/4) = O(n^2)        |   Dp table         |
