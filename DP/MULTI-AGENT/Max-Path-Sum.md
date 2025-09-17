# MAX-PATH-SUM 

- Try ON : https://www.geeksforgeeks.org/problems/path-in-matrix3805/1
- Use the multiagent dp intuition to solve with states of dp[r][c] ,

- Can also eliminate take dimension for row `r` since we only need the values & states of prev_row , just keep prev_dp for prev_row states and dp for curr row states
```
// User function Template for C++

class Solution {
  public:
    int maximumPath(vector<vector<int>>& mat) {
       int n = mat.size();
       int m = mat[0].size();
       vector<int> prev_dp(m, 0) ;
       
       for (int j = 0 ; j < m ; j++) prev_dp[j] = mat[0][j] ;
       for (int i = 1 ; i < n ; i++) {
         vector<int> dp(m, 0) ;
           
           for (int j = 0; j < m ; j++) {
               for (int dc = -1 ; dc <= 1 ; dc++) {
                   int pc = j + dc ;
                   if (pc >= 0 && pc < m) {
                       int val = prev_dp[pc] + mat[i][j] ;
                       dp[j] = max(dp[j] , val) ;
                   }
               }
           }
           prev_dp = dp ;
       }
       int res = INT_MIN ;
       for (int j = 0; j < m ; j++) res = max(res , prev_dp[j]) ;
       
       return res ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |       O(N * M )     |     For all rows . compute using the states cols of prev-rows |
| 🧠 SPACE |    O(M)        |    Dp[M]  , preev_dp[M]      |
