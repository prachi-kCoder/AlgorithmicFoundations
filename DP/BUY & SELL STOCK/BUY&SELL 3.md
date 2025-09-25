## BUY&SELL 3

- Brute Force {Dp that comes to mind : 3 states : dp[i][is_holding][t] : `i` : index , `is_holding` : stock bought or not, `t` : transactions done}
- But this undergoes TLE :

```cpp
#define ll long long
class Solution {
public:
    const int mn = LLONG_MIN ;
    vector<vector<vector<ll>>> dp ;
    // t -> 0/1/2 {at most 2 transaction allowed }! 
    int n ;
    ll solve(int i , int is_holding , int t , vector<int>& prices) {
        if (i >= n) return 0 ;
        if (t == 0 && is_holding == 0) return 0 ;// done 2 
        if (dp[i][is_holding][t] != mn ) return dp[i][is_holding][t] ;

        ll buy = mn , sell = mn , skip = mn ;
        if (is_holding == 0) {
            buy = -prices[i] + solve(i+1 , 1 , t-1 , prices) ;
        }else {
            sell = prices[i] + solve( i , 0 , t , prices ) ;
        }
        skip = solve(i + 1 , is_holding , t , prices) ;
        return dp[i][is_holding][t]  = max({buy , sell , skip}) ;
    }
    int maxProfit(vector<int>& prices) {
        n = prices.size() ;
        dp.resize(n , vector<vector<ll>>(2 , vector<ll>(3 , mn)));

        return solve(0 ,0 , 2, prices );
    }
};
```

- NOW Thingk at the end we want to make 2 transactions {Optimally make the 2 transaction with sum of P1 + P2 to be max}
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n <= 1) return  0 ;
        vector<int> left(n,0);
        vector<int> right(n,0);
        int mn = prices[0] ;
        int mx = prices[n-1] ;
 
        for (int i = 1 ,j = n-2 ; i < n && j >= 0 ; i++ ,j--) {
            left[i] = max(left[i-1] , prices[i] - mn);
            right[j] = max(right[j+1] , mx - prices[j] );
            mn =  min(mn , prices[i]);
            mx =  max(mx , prices[j]);
        }

        int ans = 0 ;
        for (int i = 0 ; i < n ; i++) {
            ans = max(ans , left[i] + right[i]) ;
        }
        return ans ;
    }
};
```
