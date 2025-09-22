# Matrix-Multiplication
##### MIN COST MATRIX MULTIPLICATION 

- Array arr[] of len N -> `(N-1)` matrices
- arr[0,1,2,3,4,5]
##### How partition is made ?:


- Mat : `arr[i-1] X arr[i] .... arr[k-1]Xarr[k]` | `arr[k+1]Xarr[k+2] .... arr[j]`
- Final Dimension: `arr[i-1]Xarr[k]`  & `arr[k]Xarr[j]`  So curr_cost = `arr[i-1] x arr[k] x arr[j]`
- And left_cost = dp[i][k]  
- And right_cost = dp[k+1][j]

- Just get the right partitions with minimum cost 
### BASE CASE
- dp[i][i] = 0
- As i start from 1 so the 1 matrix :`arr[i-1]Xarr[i]`  have 0 cost of multiplication
- here i = j means 1 chain length of 1 matrix arr[i-1]Xarr[i] only
  
- &  k -> {i to j-1 }as the last matrix right dimention is j  so right most matrix can be arr[j-1]xarr[j]
- Hence the rightmost partition = DP[k+1][j] and k at max goes upto j-1 

## MEMOIZATION
```cpp
#include <bits/stdc++.h>
using namespace std;
// mat = a[i-1]Xa[i] ;
int mcm(vector<int>& a , int i , int j ,vector<vector<int>>& dp) {
    if (j == i) return 0; // single mat (0 cost of mulitplcation)
    
    if (dp[i][j] != -1) return dp[i][j] ;
    int min_cost = INT_MAX ;
    
    for (int k = i ; k < j ; k++) {
        int c1 = mcm(a , i , k, dp);
        int c2 = mcm(a , k+1 , j, dp) ;
        int c3 = (a[i-1]*a[k]*a[j]) ; // curr_cost 
        min_cost = min((c1 + c2 + c3) , min_cost ) ;
    }
    
    return dp[i][j] = min_cost ;
}
int main() {
	vector<int> a = {1,2,3,4,3};
	int n = a.size(); 
	vector<vector<int>> dp(n , vector<int>(n , -1)) ;
	
	cout << mcm(a , 1 , n-1 , dp) << endl ;
	
	return 0 ;
}

```
## TABULATION 
```cpp
#include <bits/stdc++.h>
using namespace std;
// mat = a[i-1]Xa[i] ;
int mcm(vector<int>& a ) {
    int n = a.size();
    
	vector<vector<int>> dp(n+1 , vector<int>(n+1 , 0)) ;
	// len = 1 (i == j) dp[i][j] = 0  {single mat }
	
	for ( int len = 2 ; len <= n ; len++ ) {
	    for ( int i = 1 ; i <= n-len ; i++ ) {
	        int j = i + len - 1 ;
	        dp[i][j] = INT_MAX ;
	        
	        for (int k = i ; k < j ; k ++) {
	            int l_cost = dp[i][k] ;
	            int r_cost = dp[k+1][j] ;
	            int curr_cost = (a[i-1]*a[k]*a[j]) ;
	            dp[i][j] = min(dp[i][j] , l_cost + r_cost + curr_cost) ;
	        }
	    }
	}
    
    return dp[1][n-1] ;
}
int main() {
	vector<int> a = {1,2,3,4,3};
	int n = a.size(); 
	cout << mcm(a ) << endl ;	
	return 0 ;
}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |      O(N x N x N)    | For N lengths , i [1,n-len] , k [i , j-1]|
| 🧠 SPACE |     O(N x N)       |         Dp table   |
