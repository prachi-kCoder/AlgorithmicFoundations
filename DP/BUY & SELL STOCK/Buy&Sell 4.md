## BEST TIME TO Buy&Sell STOCK 4

- Try :https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/

# Tabulation 
```cpp

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
