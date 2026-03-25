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

# NOW  OPTIMISED VERSION :
- Iterative checking for all l_diagonal and r_diag causes TLE
- OBSERVE :
- The `main diagonal (↘)` runs from top-left to bottom-right. All cells on the same `↘ diagonal` have the same value of `i - j`
- The  `anti-diagonal (↙)` runs from top-right to bottom-left. All cells on the same `↙ diagonal` have the same value of `i + j`
- Then to avoid placing any queen check at any ith row whether the j , i-j and i+j are already occupied means same col , `↘ diagonal` ,& `↙ diagonal`  are occupied or not ie they're then not right placement .
- i-j can be negative for all i < j so to avoid `index out of bound error` we take `i-j+n-1` as if `i+j` will correctly identify in such cases and `i-j+n-1` won't give any error .

## FINAL CODE SOLUTION 
```cpp
class Solution {
    vector<vector<int>> res ;
  public:
    void solve(int r , int col_mask , int ldia , int rdia , int n , vector<int>& curr) {
        if (r >= n) {
            res.push_back(curr) ;
            return ;
        }
        
        for (int c = 0 ; c < n ; c++) {
            int bit = (1 << c) ;
            if (col_mask&bit) continue ;
            if (ldia&bit) continue ;
            if (rdia&bit) continue ;
            
            curr.push_back(c+1) ;
            solve(r+1 , col_mask|bit , (ldia|bit) << 1 , (rdia|bit) >> 1 , n , curr ) ;
            curr.pop_back();
        }
    }
    
    vector<vector<int>> nQueen(int n) {
        vector<int> curr ;
        
        solve(0 , 0 , 0 ,0, n , curr ) ;
        
        return res ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*(N!))     | Read above .  |
| 🧠 SPACE |    O(N*N) + O(N)       | Board  + Recusive stack    |




