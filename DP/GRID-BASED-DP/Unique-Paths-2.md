# UNIQUE-PATH2 {WITH OBSTACLE} 

### MEMOIZATION
```cpp
class Solution {
public:
    int dp[101][101] ;
    int countPath(int i , int j , int m , int n, vector<vector<int>>& obGrid) {
        if (i >= m || j >= n) return 0 ;
        if (i == m-1 && j == n-1) return 1 ;
        if (dp[i][j] != -1) return dp[i][j] ;
        if (obGrid[i][j] == 1) {
            return dp[i][j] = 0 ;
        }
        return dp[i][j] = countPath(i+1 , j , m ,  n , obGrid) + countPath(i , j+1 , m , n , obGrid) ;
    }
    int uniquePathsWithObstacles(vector<vector<int>>& obGrid) {
        int m = obGrid.size(); int n = obGrid[0].size();
        if(obGrid[m-1][n-1] == 1) return 0 ;
        if (m == 1 && n == 1) return 1 ;

        memset(dp , -1, sizeof(dp)); 
        return countPath( 0, 0, m , n , obGrid) ;
    }
};
```
### TABULATION 
```cpp
class Solution {
public:
    long long dp[101][101] ;
    int uniquePathsWithObstacles(vector<vector<int>>& obGrid) {
        int m = obGrid.size(); int n = obGrid[0].size();
        if (obGrid[m-1][n-1] == 1) return 0 ;
        if (m ==1 && n==1) return 1 ;
        memset(dp ,0 , sizeof(dp)) ;
        for (int i = m-1 ; i >= 0 ; i--) {
            if (obGrid[i][n-1] == 1) break ;
            dp[i][n-1] = 1;
        }
        for (int j = n-1 ; j >= 0 ; j--) {
            if (obGrid[m-1][j] == 1) break ;
            dp[m-1][j] = 1 ;
        }

        for (int i = m-2 ; i >= 0 ; i--) {
            for (int j = n-2 ; j >= 0 ;j--) {
                dp[i][j] = (obGrid[i][j]) ? 0 : dp[i][j+1] + dp[i+1][j] ;
            }
        }
        return dp[0][0];
    }
};
```
TEMPLATE :
# 🔍 Complexity Analysis
- Both memo , tabulation
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(m*n)  |   Traversal to m*n    |
| 🧠 SPACE |   O(m*n)      |     DP-TABLE       |
