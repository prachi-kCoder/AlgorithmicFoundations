# MINIMUM NUMBER OF WORK SESSIONS 

- Try : https://leetcode.com/problems/minimum-number-of-work-sessions-to-finish-the-tasks/description/
- This is TSP variation :
- TC is optimised using DP[mask][time] ;
- Brute says : Check all possible `N!` combinations of all n- tasks and compute the mini sessions , but this is IMPRACTICAL even for small n
- `Dp[mask][time]` :  Keeps the min-session cnt with a state defined by mask and the time of the ongoing session

# Memoization - Top Down approach
```cpp
class Solution {
public:
    int mn_cnt , n , session ;
    int full_mask ;
    vector<vector<int>> dp ;
    int solve(int mask ,int timer, vector<int>& tasks) {
        if (mask == full_mask) return 0 ; 
        if (dp[mask][timer] != -1) return dp[mask][timer] ;
        int ans = n ;

        for (int i = 0; i < n ; i++) {
            if (!(mask&(1<<i))){
                int nxt_mask = (mask|(1<<i));
                bool start_new = false ;
                int next_time = timer + tasks[i] ;
                if (timer == 0 || next_time > session ) {
                    start_new = true ;
                    next_time = tasks[i] ;
                }
                int c = start_new + solve(nxt_mask , next_time , tasks);
                ans = min(ans , c) ;
            }
        }

        return dp[mask][timer] = ans ;
    }
    int minSessions(vector<int>& tasks, int sessionTime) {
        n = tasks.size();
        if (n <= 1) return 1 ;
        full_mask = (1<<n)-1 ;
        // start with any task
        mn_cnt = n ;
        session = sessionTime ;
        dp.resize(full_mask + 1 ,vector<int>(sessionTime + 1 , -1)) ;

        return solve( 0 , 0 ,  tasks ) ;
    }
};
```
# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(2^n x sessionTime)   |   As all states with different session times are explored        |
| 🧠 SPACE |   O(2^n x sessionTime)        |    Dp table      |
