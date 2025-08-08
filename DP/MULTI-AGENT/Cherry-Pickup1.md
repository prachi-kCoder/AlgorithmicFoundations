# CHERRY PICKUP-1
- Try here :https://leetcode.com/problems/cherry-pickup/description/

- Rather than doing 2 DFS (Top-Left to Btm Right and Back to Top Left) , go with 2 player simultaneous DFS
### WHY so ?
- Attain global maxima , by get the max sum of cell over 2 paths 1 for forward & other one for back traversal
- if P1 , P2 over the same cells then only consider take the grid[r][c] once  . as once taken can't be taken once
- Keep in mind as soon as one of those reaches the lastcell grid[n-1][n-1] return the val , because last cell is also need to be considered at max once
- We are doing simultaneous 2 player traversal , allows us not to mark the cell from forward to last cell as 0 (taken cherry) eliminating the need to explicitly keep track of paths , unlike what is to be done in 2 dfs {start to last and back to start}
-The reason a conventional two-pass DFS (start to end, then end to start) fails to guarantee a global maximum is that the first pass makes decisions that permanently alter the grid for the second pass.
```cpp
class Solution {
public:
    int n ;
    int dp[51][51][51][51] ;
    int cherryPickup(vector<vector<int>>& grid) {
        n = grid.size();
        memset(dp , -1 , sizeof(dp)) ;
        return max(0, solve(0 ,0 , 0, 0, grid));
    }
    int solve(int r1 , int c1 , int r2 , int c2 , vector<vector<int>>& grid) {
        if (r1 >= n || c1 >= n || r2 >= n || c2 >= n ||  grid[r1][c1] == -1 || grid[r2][c2] == -1 ) {
            return INT_MIN ;
        }
        if (r1 == n-1 && c1 == n-1) {
            return grid[r1][c1] ;
        }
        if (r2 == n-1 && c2 == n-1) {
            return grid[r2][c2] ;
        }
        if (dp[r1][c1][r2][c2] != -1) return dp[r1][c1][r2][c2] ;

        int cherries ;
        if (r1 == r2 && c1 == c2) {
            cherries = grid[r1][c1] ;
        }else {
            cherries = grid[r1][c1] + grid[r2][c2];
        }
            int dd = solve(r1 + 1 , c1 , r2 + 1 , c2 , grid);
            int dr = solve(r1 + 1 , c1 , r2 , c2 + 1, grid);
            int rr = solve(r1 , c1 + 1 , r2 , c2 + 1, grid);
            int rd = solve(r1 , c1 + 1 , r2 + 1, c2 , grid);

        return dp[r1][c1][r2][c2]  = cherries + max({dd , dr , rr , rd});
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N*N*N*N)     | 2 PLAYER CONFIGURATION {r1,c2,r2,c2}  all may be explored  |
| 🧠 SPACE |   O(51*51*51*51)         |  Dp table + Rec Stack          |
