## CHERRY-PICKUP II 

- MultiAgent DP works the best as 2 robots are to be given equals chances over the reachable cherries and in order to achieve global maxima we do
- States of DP : r , c1 , c2 as both the robots in any movement will come to the next Row (that common to both) , but the dc could be {-1,0,1} hence we consider all possible combinations of columns .
 
```cpp
class Solution {
public:
    int n , m ;
    long long dp[71][71][71] ;
    long long dfs(int r , int c1 , int c2 , vector<vector<int>>& grid) {
        if (c1 < 0 || c1 >= m || c2 < 0 || c2 >= m ) return LLONG_MIN ;

        long long cherries = 0LL ;
        if (c1 == c2) {
            cherries = grid[r][c1] ;
        }else {
            cherries = grid[r][c1] + grid[r][c2] ;
        }
        if ( r == n-1 ) return cherries ;

        if (dp[r][c1][c2] != -1LL) return dp[r][c1][c2] ;
        long long mx = 0LL ;

        for (int dc1 = -1 ; dc1 <= 1; dc1++ ) {
            for (int dc2 = -1 ; dc2 <= 1 ; dc2++ ) {
                mx = max(mx , dfs(r+1 ,c1 + dc1 , c2 + dc2 , grid)) ;
            }
        }

        return  dp[r][c1][c2] = cherries + mx ;
    }
    int cherryPickup(vector<vector<int>>& grid) {
        n = grid.size() ; m = grid[0].size();
        memset(dp , -1LL , sizeof(dp)) ;

        return dfs(0 ,0, m-1 , grid) ;
    }
};
```



# 🔍COMPLEXICITY ANALYSIS

| 🔢 Metric  |	📊 Complexity | 	🧠 Why? |
|-----------|-------------|------------|
| 🧭 TIME  |     O(Nx M x M)  |   For each row r, both robots can be at any column c1 and c2, leading to N × M × M unique states. Each state explores up to 9 transitions (3 moves per robot), but constant branching doesn’t affect asymptotic complexity.    |
| 🧠 SPACE |     O(71 x 71 x 71)      |   The DP table stores results for every (r, c1, c2) triple. With constraints N ≤ 70, M ≤ 70, this fits within dp[71][71][71].       |
