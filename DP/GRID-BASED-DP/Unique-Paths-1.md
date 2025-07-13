# UNIQUE-PATHS 

# TABULATION 
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
# MEMOIZATION
```cpp
class Solution {
public:
    int dp[101][101] ; 
    int memo(int i , int j ,int m,int n ) {
        if (i >= m || j >= n) return  0 ;
        if ( i == m-1 && j == n-1) return 1 ;
        if (dp[i][j] != -1) return dp[i][j];

        return dp[i][j] = memo(i+1 , j , m , n) + memo(i , j+1, m , n) ;
    }
    int uniquePaths(int m, int n) {
        if (m == 1 ||  n==1 ) return 1 ;
        memset(dp, -1, sizeof(dp));

        return memo(0 , 0 ,m , n) ;
    }
};
```
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(n*m)       |  Precomputing for all cells    |
| 🧠 SPACE |      O(n*m)   |    DP-Table        |
