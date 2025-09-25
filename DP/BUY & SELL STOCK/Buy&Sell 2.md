# Buy&Sell 2
Try : https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

## TABULATION :{BOTTOM-UP APPROACH}
```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n , vector<int>(2 , 0)) ;
        // is_holding :1 / not_holding:0
        dp[0][0] = 0 ; // 
        dp[0][1] = (-1)*(prices[0]) ; // 
        for (int i = 1 ; i < n ; i++) {
      
            // to not to hold either sell or continue not holding
            dp[i][0] = max(dp[i-1][0] , prices[i] + dp[i-1][1]);

            // to continue holding / or to buy
            dp[i][1] = max(dp[i-1][1] , (-1)*prices[i] + dp[i-1][0]);
        }

        return dp[n-1][0] ;
    }
};
```

## MEMOIZATION : {TOP-DOWN APPROACH}
```cpp
class Solution {
public:
    const int mn = (-1)*((int)(3e4)+1) ;
    int n ;
    vector<vector<int>> dp ;
    int solve(int i , int is_holding , vector<int>& prices) {
        if (i >= n) return 0 ;
        if(dp[i][is_holding] != -1) return dp[i][is_holding] ;

        int sell = mn , buy = mn , skip = mn ;
        if (is_holding) {
            sell = prices[i] + solve(i+1 , 0 , prices);
        }else {
            buy = -1*(prices[i]) + solve(i+1 , 1 , prices ) ;
        }
        skip = solve(i+1 , is_holding , prices );
        return dp[i][is_holding] = max({sell , buy , skip});
    }
    int maxProfit(vector<int>& prices) {
        n = prices.size();
        dp.resize(n , vector<int>(2,-1)) ;

        return solve(0 , 0 , prices );
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*2)     |  For all n indices , you can compute 2 col dimension |
| 🧠 SPACE |   O(N*2)    |  O(N*2)       |
