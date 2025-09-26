# Best Time to Buy and Sell Stock with Cooldown

Try :https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/

## MEMOIZATION 
```cpp
class Solution {
public:
    const int mn = (-1)*((int)(5e6+1)) ;
    vector<vector<int>> dp ;
    int n ;
    int solve(int i , int is_holding , vector<int>& prices) {
        if (i >= n)  return 0 ;

        if (dp[i][is_holding] != mn) return dp[i][is_holding] ;

        int buy = mn , sell =  mn , skip = mn ;
        if (is_holding) {
            sell = prices[i] + solve(i+2 , 0 , prices) ;
        } else {
            buy = -prices[i] + solve(i+1 , 1 , prices) ;
        }
        skip = solve(i+1 , is_holding , prices) ;
        return dp[i][is_holding] = max({buy , sell , skip});
    }
    int maxProfit(vector<int>& prices) {
        n = prices.size();
        dp.resize(n , vector<int>(2 , mn)) ;

        return solve(0 , 0 , prices ) ;
    }
};
```
