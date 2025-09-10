## Longest Palindromic Subsequence (LPS)
- Problem: Find longest subsequence that reads the same forward and backward in one string.
- State: dp[i][j] → LPS length from index i to j in s
## TABULATION :

```cpp
If s[i] == s[j] → dp[i][j] = 2 + dp[i+1][j-1]
Else → dp[i][j] = max(dp[i+1][j], dp[i][j-1])
```

```cpp
int longestPalinSubseq(string &s) {
        int n = s.length();
        vector<vector<int>> dp(n , vector<int>(n , -1)); 
        
        for (int i = 0; i < n ; i++ ) dp[i][i] = 1 ;
        for (int len = 2 ; len <= n ; len++) {
            for (int i = 0 ; i <= n-len ; i++) {
                int j = i + len - 1 ;
                if (s[i] == s[j]) {
                    dp[i][j] = (len == 2) ? 2 : 2 + dp[i+1][j-1] ;
                }else {
                    dp[i][j] = max(dp[i+1][j] , dp[i][j-1]) ;
                }
            }
        }
        
        return dp[0][n-1] ;
```

## MEMOIZATION :

```cpp
// User function Template for C++

class Solution {
  public:
    int expand(int l , int r , string& s , vector<vector<int>>& dp) {
        if (l < 0 || r >= s.length()) return 0 ;
        if (dp[l][r] != -1) return dp[l][r] ;
        
        int take = 0 , skip = 0 ;
        if (s[l] == s[r]) {
            take = 2 + expand(l-1 , r + 1 , s, dp);
        }
        skip =  max(expand(l-1 , r  , s, dp) , expand(l , r+1 , s, dp)) ;
        return dp[l][r] = max(take , skip);
    }
    int longestPalinSubseq(string &s) {
        int n = s.length();
        vector<vector<int>> dp(n , vector<int>(n , -1)); 
        
        for (int i = 0; i < n ; i++) dp[i][i] = 1 ;
        // start and end 
        // expand from each index as centres 
        int mxLen = 1 ;
        for (int c = 0 ; c < n ; c++ ) {
            int odd = 1 + expand(c-1 , c+1, s, dp);
            int even = expand(c-1, c , s , dp);
            
            mxLen = max({mxLen , odd , even}) ;
        }
        return mxLen ;        
  }
};
```

## 🔍 Complexity Analysis

| Metric     | Complexity | Explanation |
|------------|------------|-------------|
| 🧭 Time     | O(n²)       | We fill a 2D DP table for all substrings `s[i..j]`, with `i ≤ j`, leading to ~n² transitions. |
| 🧠 Space    | O(n²)       | A 2D DP matrix of size `n × n` stores LPS values for each substring. |
