## CHECK KNIGHT CONFIGURATION

#### try on :https://leetcode.com/problems/check-knight-tour-configuration/

```cpp
class Solution {
public:
    vector<int> dr = {-2 ,-2 , -1 ,-1 , 2, 2, 1, 1} ;
    vector<int> dc = {-1 ,+1 , -2 ,+2 , -1,1,-2,2 } ;
    int n ;
    bool solve(int i , int j ,int val, vector<vector<int>>& grid) {
        if (val == n*n-1) return true ;
        int prev = grid[i][j] ;
        grid[i][j] = -1 ;

        for (int k = 0 ; k <8 ; k++ ) {
            int nr = i + dr[k] ;
            int nc = j + dc[k] ;
            if (nr >= 0 && nr < n && nc >= 0  && nc < n && grid[nr][nc] == val+1 ) {
                if (solve(nr , nc , val+1 , grid)) return true ;
            }
        }
        grid[i][j] = prev ;
        return false ;
    }
    bool checkValidGrid(vector<vector<int>>& grid) {
        n = grid.size() ;
        if (n == 1) return true ;
        if (n == 2) return false ;
        return solve(0 ,0,0, grid );
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(8*N*N) = O(N*N)         |  For every cell (r,c) we will be check for the 8 choices (loop) , but the next call will only be made if the (val + 1 )  is found at any adjacent neighbour , hence n*n cells are only visited in the scenario when all (0,n*n-1) values were found !      |
| 🧠 SPACE |    O(N*N)        |  Ans dfs depth we go upto the last cell (n*n-1) and return true from there on |
