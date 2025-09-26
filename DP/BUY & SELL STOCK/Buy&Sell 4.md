## BEST TIME TO Buy&Sell STOCK 4

- Try :https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/
- At most k transactions
  
# TABULATION :

- Important initialisations
- We init with `mn` as to avoid sell as stock not bought becoz 0 says bought at zero :`dp[i][t-1][1] =  0 ` gets wrong result so init the invalid state with `mn`
- Valid states : `dp[i][0][0] = 0` : No stock no trasaction and no profit , `dp[i][1][1] = -prices[i]` : Buy stock at ith index any ith index allowed for 1st transaction .
- t `[1 , min(k,(i+2)/2)]` ??  : As `days` upto ith index = `i+1` in d days -> at max transactions = (d+1)/2 needs to be processed  to compute the right profit, on buying or selling
- At the end : Take the max profit at any t value upto `n-1` index as any no of transaction can give max profit
  
```cpp
class Solution {
  public:
    using ll = long long ;
    const int mn = ((int)(1e6) + 1)*(-1) ;
    int maxProfit(vector<int>& prices, int k) {
        int n = prices.size();
        
        vector<vector<vector<ll>>> dp(n , vector<vector<ll>>(k+1 , vector<ll>(2 , mn)));
        
        // allowing 1st trasaction at all indices
        for (int i = 0 ; i < n ; i++) {
            dp[i][0][0] = 0 ;
            dp[i][1][1] = -prices[i] ;
        }
        
        for (int i = 1 ; i < n ; i++) {
            for(int t = 1 ; t <= min(k,(i+2)/2) ; t++) { // days = i+1 , so at mx = (days + 1)/2 transaction are to be processed
                // sell or not hold
                dp[i][t][0] = max(prices[i] + dp[i-1][t][1] , dp[i-1][t][0]);
                // hold or buy
                dp[i][t][1] = max(-prices[i] + dp[i-1][t-1][0] , dp[i-1][t][1]);
            }
        }
        
        ll res = 0 ;
        for (int t = 1 ; t <= k ;t++) {
            res = max(res, dp[n-1][t][0]) ;
        }
        return res ;
        
    }
};
```

# memoization 
```cpp
#define ll long long 
class Solution {
public:
    const int mn = (-1)*((int)1e6 + 1 );
    vector<vector<vector<ll>>> dp;
    ll solve(int i , int is_holding, int k , vector<int>& prices) {
        if (i >= prices.size()) return 0 ;
        if (k == 0 && is_holding == 0) {
            return dp[i][is_holding][k] = 0LL ;
        }
        if(dp[i][is_holding][k] != mn) return dp[i][is_holding][k] ;
        ll buy = mn , sell = mn , skip = mn ; 
        if (!is_holding) {
            buy = -prices[i] + solve(i+1 , 1 , k-1 ,prices) ;
        }else {
            sell = prices[i] + solve(i+1 , 0 , k ,prices) ;
        }
        skip = solve(i+1 , is_holding , k , prices) ;
        return dp[i][is_holding][k] = max({buy , sell , skip});
    }
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        dp.resize(n , vector<vector<ll>>(2 , vector<ll>(k+1 , mn)));

        return solve(0 , 0 , k , prices);
    }
};
```
