# Egg-Drop

### MOST OPTMISED 
- Just change the linear iteration over k -> `binary iteration` over k values

```cpp
public:
    int dp[1001][1001];
    
    int solve(int e ,int f) {
      if (f <= 1) return f ;
      if (e == 1) return f ;
      if (dp[e][f] != -1) return dp[e][f];
       
      int moves = f ;
      int l = 1 , r = f ;
      while (l < r) {
          int mid = l + (r - l) / 2;
          
          int broken = solve(e-1 , mid - 1) ;
          int not_broken = solve(e , f - mid) ;
          int curr_moves = 1 + max(broken , not_broken) ;
          moves = min(moves , curr_moves) ;
          if (broken < not_broken) {
              l++ ;
          }else{
              r-- ;
          }
      }
       
      return dp[e][f] = moves ;
    }
    int eggDrop(int e, int f) {
       if (e == 1) return f ;
        if (f <= 1) return f ;
        memset(dp ,-1, sizeof(dp)) ;
        return solve(e, f);
       
}

```

- `THESE approaches may undergo TLE {But logic is built from these 2 approaches}`

#### TABULATION :

```cpp
int egg_drop(int e , int f ) {
    if (e == 1) return f ;
    if (f <= 1) return f ;
    
    vector<vector<int>> dp(e+1 , vector<int>(f+1 , 0 )) ;
    for (int c = 1 ; c <= e ; c++) dp[c][1] = 1 ;
    for (int k = 1 ; k <= f ;k++) dp[1][k] = k ;
    
    for (int c = 2 ; c <= e ; c++) {
        for (int tf = 2 ; tf <= f ; tf ++) {// total floor 
            dp[c][tf] = INT_MAX ;
            for (int k = 1 ; k <= tf ; k++) {
                int curr = 1 + max(dp[c-1][k-1] , dp[c][tf - k]);
                dp[c][tf] = min(dp[c][tf] , curr) ;
            }
            
        }
    }
    return dp[e][f] ;
}
```

#### MEMOIZATION :

```cpp
#include <bits/stdc++.h>
using namespace std;
int dp[1001][1001];
    
    int solve(int e ,int f) {
      if (f <= 1) return f ;
      if (e == 1) return f ;
      if (dp[e][f] != -1) return dp[e][f];
       
      int moves = f ;
      for (int k = 1 ;k <= f ; k++) {
          int broken = solve(e-1 , k-1);
          int not_broken = solve(e , f-k);
          moves = min(moves , 1 + max(broken , not_broken));
      }
       
      return dp[e][f] = moves ;
    }

int main() {
	int e = 2 ;
	int f = 36 ;
	memset(dp ,-1, sizeof(dp)) ;
	
	cout << solve(e ,f) << endl ;

}

```
