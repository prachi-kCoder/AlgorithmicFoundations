# TRAVELLING SALESMEN PROBLEM 

Try : https://www.geeksforgeeks.org/problems/travelling-salesman-problem2732/1?page=3&company=Microsoft&difficulty=Hard&sortBy=submissions
### COMPLEXICITY OPTIMISATION 
- Brute force : `O(N!)` or precisely `O((N-1)!)`  actually for N cities fix starting pos = 0th nodes so the remaining N-1 cities can be arranged in (N-1)! arrangements ie how 0(n-1!)

- But with `dp[n][mask]` : All memoization allows to reuse any visited state to compute min cost from ith nodes with `mask` shows the state of visited nodes
- Computation of `dp[n][mask]`  : Min cost to reach all unvisited nodes

- Final Time Complexity: O(N x 2^n) much better that N! and feasible for n<= 20 or 25 .
- SC : O(N x 2^n) for DP table
- # TOP-DOWN
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
# btm up
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
#include <climits>

using namespace std;

const int INF = 1e9; // Infinity placeholder

// Function to solve TSP using Dynamic Programming
// n: number of cities
// dist: adjacency matrix where dist[i][j] is distance from i to j
int solveTSP(int n, const vector<vector<int>>& dist) {
    // 1 << n is 2^n. This represents all possible subsets of cities.
    // dp[mask][i] stores min cost to visit cities in 'mask' ending at city 'i'
    vector<vector<int>> dp(1 << n, vector<int>(n, INF));

    // Base case: Starting at city 0. 
    // Mask 1 (binary ...001) means only city 0 is visited.
    // Cost is 0 because we start there.
    dp[1][0] = 0;

    // Iterate through all possible masks (subsets of cities)
    for (int mask = 1; mask < (1 << n); ++mask) {
        // Try ending at every city 'i'
        for (int i = 0; i < n; ++i) {
            // If city 'i' is present in the current subset (mask)
            if ((mask & (1 << i))) {
                
                // Try coming to 'i' from every other city 'j'
                for (int j = 0; j < n; ++j) {
                    // If city 'j' is in the mask and j != i
                    if ((mask & (1 << j)) && j != i) {
                        
                        // Previous state: mask without city 'i'
                        int prevMask = mask ^ (1 << i);
                        
                        // Update minimal cost
                        if (dp[prevMask][j] != INF) {
                            dp[mask][i] = min(dp[mask][i], dp[prevMask][j] + dist[j][i]);
                        }
                    }
                }
            }
        }
    }

    // Final answer calculation:
    // We have visited all cities (mask = all 1s) and need to return to start (city 0)
    int finalMask = (1 << n) - 1;
    int minCost = INF;

    for (int i = 1; i < n; ++i) {
        if (dp[finalMask][i] != INF) {
            // Cost to visit all ending at 'i' + cost to return to 0
            minCost = min(minCost, dp[finalMask][i] + dist[i][0]);
        }
    }

    return minCost;
}

int main() {
    // Example: 4 cities
    int n = 4;
    
    // Adjacency matrix representing distances
    // dist[i][j] is the distance from city i to city j
    vector<vector<int>> dist = {
        {0, 20, 42, 25},
        {20, 0, 30, 34},
        {42, 30, 0, 10},
        {25, 34, 10, 0}
    };

    cout << "Minimum Cost to visit all cities: " << solveTSP(n, dist) << endl;

    return 0;
}
```
