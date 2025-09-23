# SCS(Shortest-common-supersequence)

- Try now :https://www.geeksforgeeks.org/problems/shortest-common-supersequence0322/1?page=7&company=Microsoft&difficulty=Medium,Hard&sortBy=submissions
- 
`SCS(s1, s2) = s1.length() + s2.length() - LCS(s1, s2)`

```cpp
int shortestCommonSupersequence(string &s1, string &s2) {
  
        int n1 = s1.length();
        int n2 = s2.length();
        // depends on lcs of s1, s2 
        vector<vector<int>> dp(n1 + 1 , vector<int>(n2+1 , 0)) ;
        int mn = min(n1 , n2) ;
        int mx = max(n1 , n2) ;
        
        for (int i = 1 ; i <= n1 ; i++ ) {
            for (int j = 1 ; j <= n2 ;j++) {
                if (s1[i-1] == s2[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + 1 ;
                    if (dp[i][j] == mn ) return mx ;
                }else {
                    dp[i][j] = max( dp[i-1][j] , dp[i][j-1] ) ;
                }
            }
        }
        int diff = mn - dp[n1][n2]  ;
        
        return mx + diff ;// bigger string and complete lcs of s1,s2
        
    }
```

- TC : O(N1 x N2)
- SC : O(N1 X N2)
