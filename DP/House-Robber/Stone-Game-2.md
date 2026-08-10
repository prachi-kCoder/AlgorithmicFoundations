## Stone-Game-2

```cpp
 Recurrence = (TOTAL_SUM_OF_P2 from i->end) - (next player's optimal score)
-> Keep in mind total_sum of P1 from i to end ie taken by SUFFIX[i]  , dp[next_i][next_m] => Next player's optimal score !
```

```cpp
#include <vector>
#include <numeric>
#include <algorithm>

using namespace std;

class Solution {
    int solve(int i, int m, const vector<int>& suffix, vector<vector<int>>& dp) {
        int n = suffix.size() - 1;
        if (i >= n) return 0;
        
        // If we can take all remaining piles in one go, take them all
        if (i + 2 * m >= n) return suffix[i];

        if (dp[i][m] != -1) return dp[i][m];

        int max_stones = 0;

        for (int x = 1; x <= 2 * m; x++) {
            int next_i = i + x;
            int new_m = max(m, x);
            
            // Your stones = All remaining stones - Opponent's optimal stones
            int curr_stones = suffix[i] - solve(next_i, new_m, suffix, dp);
            
            max_stones = max(max_stones, curr_stones);
        }

        return dp[i][m] = max_stones;
    }

public:
    int stoneGameII(vector<int>& piles) {
        int n = piles.size();
        vector<int> suffix(n + 1, 0);
        
        // Precalculate Suffix Sums
        for (int i = n - 1; i >= 0; i--) {
            suffix[i] = suffix[i + 1] + piles[i];
        }

        vector<vector<int>> dp(n, vector<int>(n + 1, -1));

        return solve(0, 1, suffix, dp);
    }
};
```
