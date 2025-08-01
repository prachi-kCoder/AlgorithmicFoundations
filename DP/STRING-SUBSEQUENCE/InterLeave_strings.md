# INTERLEAVED STRING 
- From s1 , s2 -> get s3

```cpp
bool isInterleave(string& s1, string& s2, string& s3) {
       int n  = s1.length();
       int m  = s2.length();
       if (n+m != s3.length()) return false ;
        
        vector<vector<bool>> dp(n+1 , vector<bool>(m + 1, false)) ;
        
        dp[0][0] = true ;
        
        for (int i = 1 ; i <= n ; i++) {
            dp[i][0] = (s1[i-1] == s3[i-1] && dp[i-1][0]) ; // j = 0 so k = i-1 , s1 and s3 should match (if len of s2 = 0)
        }
        for (int j = 1 ; j <= m ; j++) { 
            dp[0][j] = (s2[j-1] == s3[j-1] && dp[0][j-1]) ;// i = 0 so k = j-1  s2 and s3 should match (if len of s1 = 0)
        }
        for (int i = 1;  i <= n ; i++) {
            for (int j = 1 ; j <= m ; j++) {
                int k = i + j - 1 ;
                bool f = ((s1[i-1] == s3[k]) && dp[i-1][j]);
                bool sec = ((s2[j-1] == s3[k]) && dp[i][j-1]);
                dp[i][j] = (f||sec) ;
            }
        }
       return dp[n][m];
        
    }
```

## MEMo :
```cpp
bool solve(int i , int j ,int k, string& s1 , string& s2 , string &s3, vector<vector<int>>& dp) {
        if (i == n && j == m) return true ;
        if (k >= n+m && (i < n || j < m)) return false ;
        if (i < n && j < m && dp[i][j] != -1) return dp[i][j] == 1 ;
        
        bool f = false , sec = false ;
        
        if (i < n  &&  (s1[i] == s3[k])) {
            f =  solve(i + 1 , j, k+1 , s1,  s2 , s3, dp );
        }
        if( j<m && s2[j] == s3[k]) {
            sec =  solve(i , j+1, k+1 , s1,  s2 , s3, dp );
        }
        dp[i][j] = (f || sec) ? 1 : 0 ;
        
        return  ( f||sec );
    }
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N*M)   | Each DP cell dp[i][j] is computed once based on previous states, i.e., linear scan across n and m.   |
| 🧠 SPACE |  O(N*M)         | Tab, Table!            |
