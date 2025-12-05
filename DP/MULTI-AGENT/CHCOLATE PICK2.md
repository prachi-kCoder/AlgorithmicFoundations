# CHOCOLATE-PICKUP 2 

#### Keep in mind dp is made over steps (N+M-2) in total
`Dp state = dp[t][r1][r2]`
`r1 + c2 = t = r2 + c2`
- That is both takes equals no of steps in total N + M - 2 steps
- Here
- Constrainst :-1<= mat[i][j] <= 100
- -1 -> Invalid or Unreachable states


```cpp
class Solution {
public:
    int chocolatePickup(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        int N = n, M = m;

        const int NEG = -1e9;

        int K = N + M - 2;

        vector<vector<vector<int>>> dp(K+1,
            vector<vector<int>>(N, vector<int>(N, NEG)));

        dp[0][0][0] = grid[0][0];

        for(int k = 1; k <= K; k++) {
            for(int r1 = 0; r1 < N; r1++) {
                int c1 = k - r1;
                if(c1 < 0 || c1 >= M || grid[r1][c1] == -1) continue;

                for(int r2 = 0; r2 < N; r2++) {
                    int c2 = k - r2;
                    if(c2 < 0 || c2 >= M || grid[r2][c2] == -1) continue;

                    int best = NEG;

                    // 4 transitions
                    best = max(best, dp[k-1][r1][r2]);           // both from left
                    if(r1 > 0)
                        best = max(best, dp[k-1][r1-1][r2]);     // r1 from up
                    if(r2 > 0)
                        best = max(best, dp[k-1][r1][r2-1]);     // r2 from up
                    if(r1 > 0 && r2 > 0)
                        best = max(best, dp[k-1][r1-1][r2-1]);   // both from up

                    if(best < 0) continue;

                    int val = grid[r1][c1];
                    if(r1 != r2) val += grid[r2][c2]; // avoid double pick

                    dp[k][r1][r2] = best + val;
                }
            }
        }
        return max(0, dp[K][N-1][N-1]);
    }
};

```
