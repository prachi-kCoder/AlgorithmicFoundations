# LRS (Longest Repeating Subsequence)

##### Similar to DP , but the only difference here is we only have 1 string 
- Now the question arise lcs of 1 string with itself ?? Won't it be the whole string as its the same
- But the condition for matching any 2 indices of repeating subsequence is that the i , j (indices should not match)
- Assume it as taking LCS of 2 identical string , such that their character matching but those whose appearance index is different .

### POINT OF FAILURE :
#### ATTENTION !!
```cpp
### this is wrong !!

if (i!=  j) {
  if (s[i-1] == s[j-1]) {
     dp[i][j] = dp[i-1][j-1] + 1 ;
  }else {
     dp[i][j] = max( dp[i-1][j] , dp[i][j-1] )  ;
  }
}
### this is RIGHT!!

  if (i!=  j && s[i-1] == s[j-1]) {
     dp[i][j] = dp[i-1][j-1] + 1 ;
  }else {
     dp[i][j] = max( dp[i-1][j] , dp[i][j-1] )  ;
  }
 // DP should propagate the lrs values further so that in upcoming i, j values if i!= j  , with s[i-1] = s[j-1] then dp[i-1][j-1]  should have the max values of lrs lengths  :{ Because the non-match case still contributes to the LCS dynamic buildup}


```

```cpp
class Solution {
  public:
    int LongestRepeatingSubsequence(string &s) {
        // Simply a variation of lcs , but instread of 2 different strings we have 1 string so ensure the ith and ith indexes don't match
        
        int n = s.length();
        vector<vector<int>> dp(n+1 , vector<int>(n+1 , 0)) ;
        // i = 0 || j== 0 so lrs = 0
        for (int i = 1; i <= n ; i ++) {
            for (int j = 1 ; j <= n ; j++) { // the start index = 1 allows any character from sub1 to match any index < i  {Belonging to overlapping region of subsequence} so its necessary
                if ( i!= j && s[i-1] == s[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + 1 ;
                }else {
                    dp[i][j] = max(dp[i-1][j] , dp[i][j-1]);
                }
            }
        }
        
        return dp[n][n] ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N*N)     | i , j Domain :[1 , n]    |
| 🧠 SPACE |  O(N*N)        |  DP Table    |
