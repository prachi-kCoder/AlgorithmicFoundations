## Count-Numbers-[L,R]{diff in even& odd digits}.md

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<vector<vector<int>>>> dp;
int n;
const int OFFSET_CONST = 9 * 18; // For a number up to 18 digits.

int solve(int i, bool tight, bool is_leading_zero, const string& s, int diff) {
    if (i == n) {
        // Only count if it's not the number 0
        return (!is_leading_zero && diff > 0) ? 1 : 0;
    }

    // Correct DP state indexing with an offset
    int pos_d = diff + OFFSET_CONST;
    if (dp[i][tight][is_leading_zero][pos_d] != -1) {
        return dp[i][tight][is_leading_zero][pos_d];
    }

    int count = 0;
    int limit = tight ? (s[i] - '0') : 9;

    for (int d = 0; d <= limit; ++d) {
        if (is_leading_zero && d == 0) {
            // Recurse for leading zeros; diff remains 0.
            count += solve(i + 1, (tight && (d == limit)), true, s, 0);
        } else {
            // This is the first non-zero digit, or subsequent digits.
            int new_diff = diff;
            if (d % 2) { // Odd digit
                new_diff -= d;
            } else { // Even digit
                new_diff += d;
            }
            count += solve(i + 1, (tight && (d == limit)), false, s, new_diff);
        }
    }

    return dp[i][tight][is_leading_zero][pos_d] = count;
}
int solve_count(int num) {
    if (num <= 0) return 0;
    string s = to_string(num);
    n = s.length();
    
    // Total states for diff: 2 * OFFSET + 1
    dp.assign(n, vector<vector<vector<int>>>(2, vector<vector<int>>(2, vector<int>(2 * OFFSET_CONST + 1, -1))));
    
    return solve(0, true, true, s, 0);
}

int main() {
    int l, r;
    cin >> l >> r;
    int r_cnt = solve_count(r);
    int l_cnt = solve_count(l - 1);
    cout << "Count of [l,r] : " << (r_cnt - l_cnt) << endl;
    return 0;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(Nx2x2x(18*9*2)) | For at max numbers upto 18 digits {the diff }: dimension 4 {2*(18*9)}  , and binary state {is_leading_0 , tight} , i (for position)          |
| 🧠 SPACE |     O(Nx2x2x(18*9*2))     |   DP Table   |
