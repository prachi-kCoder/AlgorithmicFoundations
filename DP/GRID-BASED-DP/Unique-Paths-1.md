# UNIQUE-PATHS 

```cpp
class Solution {
public:
    int dp[101][101] = {0}; 
    int uniquePaths(int m, int n) {
        // Last Row
        for (int j = n-1 ; j >= 0 ; j--) {
            dp[m-1][j] =  1 ;
        }
        // Last Col
        for (int i = m-1 ; i >= 0 ; i--) {
            dp[i][n-1] =  1 ;
        }
        for (int i = m-2 ; i >= 0 ; i--) {
            for (int j = n-2 ; j >= 0 ; j--) {
                dp[i][j] = dp[i][j+1]  + dp[i+1][j]  ;
            }
        }

        return dp[0][0] ;
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(n*m)       |  Precomputing for all cells    |
| 🧠 SPACE |      O(n*m)   |    DP-Table        |
