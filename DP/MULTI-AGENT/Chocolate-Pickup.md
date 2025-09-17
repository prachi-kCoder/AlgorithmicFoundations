## Chocolate-Pickup.md

- Multiagent approach is  necessary to check all possible combinations and states of cols of R1,R2
- `Keep in mind if both R1,R2 in same col then add that val grid[r][c1]  only once`

```cpp
class Solution {
  public:
    int dp[71][71][71] ;
    
    const int mn = (int)70*70*(-100) ;
    int solve(int n, int m, vector<vector<int>>& grid) {
        // code here
        memset(dp , mn, sizeof(dp)) ;
        
        dp[0][0][m-1] = grid[0][0] + grid[0][m-1] ;
        int mx = 0 ;
        for (int r = 1 ; r < n ; r++) {
            for (int c1 = 0 ; c1 < m ; c1++) {
                for (int c2 = 0 ; c2 < m ; c2++) {
                    
                    for (int dc1 = -1 ;dc1 <= 1 ; dc1++) {
                        for (int dc2 = -1 ;dc2 <= 1 ; dc2++) {
                            
                            int pc1 = c1 + dc1 ; int pc2 = c2 + dc2 ;
                            if (pc1 >= 0 && pc1 <m && pc2 >= 0 && pc2 < m) {
                                int val = dp[r-1][pc1][pc2] + grid[r][c1]  ;
                                if (c1 != c2) {
                                    val +=  grid[r][c2] ;
                                }
                                dp[r][c1][c2] = max(dp[r][c1][c2] , val);  
                                if (r == n-1) {
                                    mx = max(mx , dp[r][c1][c2]);
                                }
                            }
                        }
                    }
                }
            }
        }
        
        return mx ;
    }
};
```

