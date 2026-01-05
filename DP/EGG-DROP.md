
## naive V/S inverse DP
```
In the naive DP , we fix floor and try all possible drops , => O(E.F^2) as we have inner loop to select the kth floor to cover the worst case
INVERSE DP : flips perspective , 'minimum no. of m moves with e eggs ? loop of moves is outer {to make reach the f floor in min moves with given e eggs}
The recurrence : dp[e][m] = dp[e-1][m-1] + dp[e][m-1] + 1  floors  , EGG BREAKS so counts the count floor belor, EGG survive then floor about & +1 for curr floor .
this BRANCHING structure  means coverage grows like binomial coefficient with increasing egg counts => exponential growth
2^m >= f  => log2m >= f  so the complexicity O(E.log2m) nearly , so O(E.moves) is much faster than O(E.F^2)
 then space optimisation with 1D dp 
```
```cpp
#include <bits/stdc++.h>
using namespace std;
// naive 
int min_moves(int e , int f) {
    if (e == 0) {
        if (f == 0) return 0 ;
        else return -1 ;
    }
    vector<vector<int>> dp(e + 1 , vector<int>(f + 1 , INT_MAX));
    dp[0][0] = 0 ;
    // 1 eggs
    for (int j = 1 ; j <= f ; j++) {
        dp[1][j] = j ; // base case -> accounting for the worst case  
    }
    for (int i = 1 ; i <= e ; i++) {
        dp[i][0] = 0 ; // 0 floor 
        dp[i][1] = 1 ; // 1 floor
    }
    
    for (int i = 2 ; i <= e ; i++) {
        for (int j = 2 ; j<= f ; j++){
            // make choice of floor
            for (int k = 1 ; k <= j ; k++) {
                int egg_breaks = dp[i-1][k-1] ;
                int egg_survive = dp[i][j-k] ;
                int worst_case = max(egg_survive , egg_breaks ) + 1 ;
                dp[i][j] = min(dp[i][j] , worst_case) ;
            }
        }
    }
    
    return  dp[e][f];
}
// inverse DP 
int min_moves2(int e , int f) {
     if (e == 0) {
        if (f == 0) return 0 ;
        else return -1 ;
    }
    // check of the min_moves to as soon as f floor is reached break !
    int max_moves = f ;
    vector<vector<int>> dp(e + 1 , vector<int>(max_moves + 1 , 0));
    for (int i = 1 ; i <= e ;i++) dp[i][1] = 1 ;// 1 move 
    for (int j = 1 ; j <= f ;j++) dp[1][j] = j ;// 1 egg 
    
    int mn_moves = -1 ;
    
    for (int m = 2 ; m <= f ; m++) {
        for (int i = 2 ; i <= e ; i ++) {
            int egg_breaks = dp[i-1][m-1] ;
            int egg_survive = dp[i][m-1] ;
            int total_f = egg_breaks + egg_survive + 1 ;
            dp[i][m] = total_f ;
            if (dp[i][m] >= f) {
                mn_moves = m ;
                break; 
            }
        }
        
        if (mn_moves != -1) break ;
    }
    
    return mn_moves ;
}
int main() {
    int e = 2 ;
    int f = 36 ;
    //naive 
    cout << min_moves(e , f) << endl ;
    cout << min_moves2(e , f) << endl ;
    return 0 ;
}

```
