# TRAVELLING SALESMEN PROBLEM 

Try : https://www.geeksforgeeks.org/problems/travelling-salesman-problem2732/1?page=3&company=Microsoft&difficulty=Hard&sortBy=submissions
### COMPLEXICITY OPTIMISATION 
- Brute force : `O(N!)` or precisely `O((N-1)!)`  actually for N cities fix starting pos = 0th nodes so the remaining N-1 cities can be arranged in (N-1)! arrangements ie how 0(n-1!)

- But with `dp[n][mask]` : All memoization allows to reuse any visited state to compute min cost from ith nodes with `mask` shows the state of visited nodes
- Computation of `dp[n][mask]`  : Min cost to reach all unvisited nodes

- Final Time Complexity: O(N x 2^n) much better that N! and feasible for n<= 20 or 25 .
- SC : O(N x 2^n) for DP table 
```cpp
class Solution {
  public:
    int n , full_mask ;
    vector<vector<int>> dp ;
    const int mx = (400*(1e3)) ;
    int dfs(int node , vector<vector<int>>& cost , int mask) {
        
        if (mask == 0) {
            return cost[node][0] ;// reverse edge to reach 0 back ;
        } 
        if (dp[node][mask] != mx) return dp[node][mask] ;
        int ans = INT_MAX ;
        
        // more unvisited neighbours to visit
        for (int j = 1 ; j < n ; j++ ) {
            if (mask&(1<<j)) {
                int new_mask = (mask^(1<<j)) ;
                int nxt = cost[node][j] + dfs(j , cost , new_mask ) ;
                ans = min(ans , nxt) ;
            }
        }

        return dp[node][mask] = ans  ;
    }
    int tsp(vector<vector<int>>& cost) {
        n = cost.size() ;
        full_mask = (1<<n) - 1 ;
        if (n == 1) return  cost[0][0];
        dp.resize(n , vector<int>(full_mask + 1 , mx)) ;
        int res = INT_MAX ;
        full_mask = (full_mask^(1)) ;
        for (int i = 1 ; i < n ; i++) {
            int mask = (full_mask^(1<<i)) ;
            int c =  cost[0][i] + dfs(i , cost , mask ) ;
            res = min(c , res) ;
        }
        return res ;
    }
};
```
