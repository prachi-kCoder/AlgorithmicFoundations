# Matrix-Multiplication
##### MIN COST MATRIX MULTIPLICATION 
- Cost for 2 matrix `A1 (axb)` , `A2(cxd)` => Cost = `axbxd`
- Final matrix order after multiplication => `(axd)`
- arr = {1,2,3,4,5}  for n = 5  , 4 matrices : `a[i-1]Xa[i]` at all i {1 , n-1}

- `k` : iterator to make the right partition so that the cost of the whole chain is minimised
- That is for all `k` `(1, n-1)` :
  
|Left Cost  |   CurrCost | Right Cost|
|-------------|----------|-------------|
| mat[i  to k] | {CurrCost} | mat[k+1 to j] |
| (a[i-1]xa[i] ) X (a[k-1]xa[k]) | a[i-1] x a[k] x a[j] | (a[k]xa[k+1]) X (a[j-1]xa[j]) |
|	a[i-1]xa[k] 	|  -> CurrCost <- | a[k] * a[j] |


- Curr cost 
- Mini mise the total cost check all partitions

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
