# 0-1 KNAPSACK 

### 1D Optimised 
- In 0/1 Knapsack, each item can be used at most once, so we must ensure we do not reuse an item multiple times. But your loop structure .

```cpp
int knapsack(int W, vector<int> &val, vector<int> &wt) {
        int n = val.size();
        vector<int> dp(W+1 , 0) ;
        for (int i = 1 ; i <= n ; i++) {
            for (int j = W ; j >= wt[i-1] ; j-- ) {
                dp[j] = max(val[i-1] + dp[j-wt[i-1]] , dp[j] ) ;
            }
        }
        
        return dp[W] ;
    }
```
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n*wt)   |      O(n*wt)   |
| 🧠 SPACE |  O(n*wt)      |  2D table |
