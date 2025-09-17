# 
- Give your best !!
- Try here : https://www.geeksforgeeks.org/problems/gold-mine-problem2608/1

- Here you don't have multiple agents though , but the intuition is the same just the dimension are reversed in order
- Since we only need the state of prev col/row in such problems we can do space optimisation just be keep the prev states to compute the curr state of dp;

```
  class Solution {
  public:
    
    int maxGold(vector<vector<int>>& mat) {
        // towards right is fixed
        int n = mat.size();
        int m = mat[0].size();
        // keep states or prev col for next row
        vector<int> prev_dp(n);
        for (int i = 0; i < n ; i++) prev_dp[i] = mat[i][0] ;
        
        
        int res = INT_MIN ;
        
        for (int j = 1 ; j < m ; j++) {
            vector<int> dp(n , 0) ;
            for (int i = 0; i < n ; i++) {
                for (int dr = -1 ; dr <= 1 ; dr++) {
                    int pr = i + dr ;
                    if (pr >= 0 && pr < n) {// valid row index
                        int val = prev_dp[pr] + mat[i][j] ;
                        dp[i] = max(dp[i], val) ;
                    }
                }
            }
            prev_dp = dp ;
        }
        // for last col
        for (int i = 0; i < n; i++) {
            res = max(res, prev_dp[i]);
        }

        
        return res ;
    }
};

```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N*M)      | For each column , you iterate over all rows , and for each , you check up to 3 adjacent rows (, , ). Since the number of rows is  and columns is , this results in  overall. |
| 🧠 SPACE |     O(N)       |   Prev_dp, dp arrays         |
