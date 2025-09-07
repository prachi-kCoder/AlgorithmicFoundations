# N-QUEENS {MAX-SCORE PLACEMENT}

- Here in 8x8 chess board place 8 queens safely where board[i][j] have positive values , return the max score of safe placements of queens
- Here common pitfall is check for the out of bounds
- While checking for left_up_dia, right_up_dia , vertically_up dia :` if (c < 0 || c >= 8) continue;` this is crucial

- As `int c = j - (i-r);`  for i = r  : c = j   &  i = 0 c : j - i   so the range :`{j,j-i}`

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
int board[8][8] ;
ll mx_score ;
bool up_safe(int i, int j) {
    for (int r = i ; r >= 0 ; r--) {
        if (board[r][j] == -1) return false ;
    }
    return true ;
}
bool left_dia(int i, int j) {
    for (int r = i ; r >= 0 ; r--) {
        int c = j - (i-r);
        if (c < 0 || c >= 8) continue;
        if (board[r][c] == -1) return false ;
    }
    return true ;
}
bool right_dia(int i, int j) {
    for (int r = i ; r >= 0 ; r--) {
        int c = j + (i-r);
         if (c < 0 || c >= 8) continue;
        if (board[r][c] == -1) return false ;
    }
    return true ;
}
void solve(int i ,  ll score) {
    if (i >= 8 ) {
        // cout << "Score :" << score << endl ;
        mx_score = max(mx_score , score);
        return ;
    }
    for (int j = 0 ; j < 8 ; j++) {
        if (!up_safe(i, j)) continue ;
        if (!left_dia(i,j)) continue ;
        if (!right_dia(i,j)) continue ;
        int val = board[i][j] ;
        board[i][j] = -1 ;
        solve(i+1 ,  score + val ) ;
        board[i][j] = val ;
    }
}
int main() {
    int t ;
    cin >> t ;
    // check all safe placements and maximise the score
    while (t-- > 0)  {
        for (int i = 0 ; i < 8 ; i++) {
            for (int j = 0 ; j < 8 ; j++) {
                cin >> board[i][j] ;
            }
        }
        
        mx_score = 0 ;
        solve( 0 , 0LL);
        cout << mx_score << endl ;
    }
    return 0;
}
```
### COMMON CONFUSION :-
- TIME-COMPLEXICITY : O(N^N) OR O(N!)  -> Its O(N!)
`Why ?` :
- O(N^N) compexicity would imply that for each of the N rows, you are trying to place a queen in any of the N columns, and you do this for every possible combination without any pruning. This would be the case if you were just brute-forcing every single cell combination
- But for :O(n!) :You're placing one queen per row, and each queen must go in a unique column (no two queens in the same column). So the problem becomes a permutation of column choices across rows.
- 🔁 Row-by-Row Placement
- Row 0: You have N choices (any column).
- Row 1: You have N−1 choices (one column is taken).
- Row 2: You have N−2 choices (tow column are taken) .
- ...
- Row N−1: Only 1 column left.

  Total number of configurations : `N x (N - 1) x (N - 2)x ...x 1= N!`
  
  In every recursive call since left_dia , right_dia , upper cols are checked hence it becomes : `N*(N!)`
  
# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*(N!))     | Read above .  |
| 🧠 SPACE |    O(N*N) + O(N)       | Board  + Recusive stack    |
