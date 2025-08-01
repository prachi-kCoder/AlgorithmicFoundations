## Longest Palindromic Subsequence

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

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(n*n)      |  for every ith index, all n index visit in worst case |
| 🧠 SPACE |  O(n*n)    | DP Table  |
