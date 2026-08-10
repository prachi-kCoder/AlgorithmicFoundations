# Stone_Game-4

```cpp
class Solution {
    vector<int> dp ;
    int solve(int n , vector<int>& dp ) {
        if (n == 0) return 0 ; // lose 

        if (dp[n] != -1) return dp[n] ;
        bool can_win = false ;

        for (int j = 1 ; 1LL * j * j <= n ; j++ ) {
            if (!solve(n -  j * j , dp)) {
                can_win = true ;
                break ;
            }
        }
        return dp[n] = can_win ? 1 : 0 ;
    }
public:
    bool winnerSquareGame(int n) {
        // dp.clear();
        // dp.resize(n+1 , -1) ; // 0 / 1 {-1 in case no explored yet!}
        vector<int> dp(n+1 , -1) ;
        dp[0] = 0 ;

        for (int i = 1 ; i <= n ; i++ ) {
            bool can_win = false ;

            for ( int j = 1 ; j * j <= i ; j++ ) {
                if (dp[i - (j*j)] == 0) { // next_player_can't win!
                    can_win = true ;
                    break ;
                }
            }
            if (can_win) dp[i] = 1 ;
            else dp[i] = 0 ;
        }

        return dp[n] == 1 ;
    }
};
```
