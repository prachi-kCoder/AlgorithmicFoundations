# LONGEST COMMON SUBSTRING


```cpp
int longestCommonSubstr(string& s1, string& s2) {
        int n = s1.length() ;
        int m = s2.length() ;
        if (n < m) return longestCommonSubstr(s2 ,s1) ;
        int len = 0 ;
        
        vector<int> prev_dp(m+1) , dp(m+1) ;
        for (int i = 1 ; i <= n ; i++) {
            for (int j = 1 ; j <=m  ; j++) {
                if (s1[i-1] == s2[j-1]) {
                    dp[j] = prev_dp[j-1] + 1 ;
                    len = max(len , dp[j]) ;
                }
            }
            prev_dp = dp ;
            dp.assign(m+1, 0) ;
        }
        
        return len ;
    }
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*M)       |  Every ith index check for it place in LCS        |
| 🧠 SPACE |  O(M)   |     1-D DP       |
