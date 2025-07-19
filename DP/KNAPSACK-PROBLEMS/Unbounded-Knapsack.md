# UNBOUNDED - KNAPSACK
- here ITEMS  have no limited quantity can choose it mulitple time

### TABULATION : (2D)
```cpp
int knapSack(vector<int>& val, vector<int>& wt, int cap ) {
        // code here
        int n = val.size() ;
        
        vector<vector<int>> dp(n + 1 , vector<int>(cap + 1 , 0LL)) ;
        for (int i = 1 ; i <= n ; i++) {
            for (int j = 1 ; j <= cap ; j++) {
                if ( wt[i-1] <= j ) {
                    dp[i][j] = max(val[i-1] + dp[i][j - wt[i-1]] , dp[i-1][j]);
                }else {
                    dp[i][j] = dp[i-1][j] ;
                }
            }
        } 
        return dp[n][cap]  ;
    }
```
### MORE OPTIMISED : (1D)
- 🔁 Loop Order Matters in Unbounded Knapsack
- Correctly chose j (capacity) as the outer loop and i (items) as the inner loop.
- This ensures each capacity j gets a chance to consider all items, even repeatedly — aligning with the "unbounded" nature.

```cpp
int knapSack(vector<int>& val, vector<int>& wt, int cap ) {
       // code here
        int n = val.size() ;
        vector<int> dp(cap + 1 , 0) ;
        for (int j = 0 ; j <= cap ; j++ ) {
            for (int i = 1 ; i <= n ; i++) {
                if ( wt[i-1] <= j ) {
                    dp[j] = max(dp[j] , val[i-1] + dp[j-wt[i-1]] ) ;
                }
            }
        }
        
        return dp[cap]  ;
    }
```


# 🔍 Complexity Analysis
### 1D
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N*M)     | For all n items , j capacity |
| 🧠 SPACE |     O(M)   |  Only for capacity  |
