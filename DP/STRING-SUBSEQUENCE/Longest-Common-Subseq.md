
# Longest-Common-Subseq 


- Space optimisation : we keep the lcs length for i-th index {prev_dp} as that is what is lcs length
- MATCH CASE : `s1[i-1] == s2[j-1]`  : dp[i][j] = dp[i-1][j-1] + 1   => for (i-1)th results look into prev_dp so prev_dp[j-1] + 1 {successfully extends } 
- Not Match CASE : `s1[i-1] != s2[j-1]`  : dp[i][j] = max(dp[i-1][j] , dp[i][j-1]) 
-   for (i-1)th result : dp[i-1][j] -> prev_dp[j]  for (i-1)th index results 
-   for (j-1)th result : dp[i][j-1] -> dp[j-1]   for curr ith index

```cpp
class Solution {
  public:
    int lcs(string &s1, string &s2) {
        int n = s1.length() ;
        int m = s2.length() ;
        if (n < m) return lcs(s2 ,s1) ;
        
        vector<int> dp(m + 1 , 0) ;
        vector<int> prev_dp(m+1 , 0) ;
        for (int i = 1 ; i <= n ; i++) {
            for (int j = 1 ; j <= m ; j++) {
                if (s1[i-1] == s2[j-1]) {
                    dp[j] = prev_dp[j-1] + 1 ;
                }else {
                    dp[j] = max(prev_dp[j] , dp[j-1]) ;
                }
            }
            prev_dp = dp ;
            dp.assign( m + 1 , 0) ;
        }
        
        return prev_dp[m] ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N*M)   |  for all i ch -> match to jth character   |
| 🧠 SPACE |      O(M)      | Only keep the len of lcs in 1Dimension , using prev_dp , dp     |
