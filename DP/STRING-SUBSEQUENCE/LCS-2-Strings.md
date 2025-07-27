# LCS : (2 STRINGS)

### TABULATION (Bottom Up Approach) :
```cpp
#include <bits/stdc++.h>
using namespace std;
int lcsLen(const string& s1 ,const string& s2) {
    int n = s1.length(); int m = s2.length();
    vector<vector<int>> dp(n+1 , vector<int>(m+1 , 0)) ;
    
    for(int i = 1 ; i <= n ; i++) {
        for (int j = 1 ; j <= m ;j++) {
            if (s1[i-1] == s2[j-1]) {
                dp[i][j] = dp[i-1][j-1] + 1;
            }else {
                dp[i][j] = max(dp[i][j-1] , dp[i-1][j] );
            }
        }
    }
    return dp[n][m] ;
}
int main() {
	string s1 = "tlkgregfna"; 
	string s2 = "tgkdmnogrkefn";
	// LCS
	cout << lcsLen(s1 , s2) << endl ;
}

```
#### YOU MAY ALSO ENCOUNTER AN INTERSTING VARIATION OF IT : TO OBTAIN LCS
```cpp
 // Reconstructing the lcs by retracking
    string lcs = "" ;
    int i = n ; int j = m ;
    while (i > 0 && j > 0) {
        if (s1[i-1] == s2[j-1]) {
            lcs += s1[i-1] ;
            i--; j-- ; // diagonal Left + UP movement in dp Table 
        }else if (dp[i-1][j] > dp[i][j-1]) { // Up move in Table 
            i-- ;
        }else {
            j-- ; // Left Move 
        }
    }
    reverse(lcs.begin() , lcs.end()) ;
    cout << "LCS is :" << lcs << endl ;
```

#### MEMOIZATION APPROACH : 
```cpp
#include <bits/stdc++.h>
using namespace std;
int solve(int i , int j , int n , int m, const string& s1 , const string& s2, vector<vector<int>>& dp) {
    if (i >= n || j >= m) return  0 ;
    
    if (dp[i][j] != -1) return dp[i][j] ;
    
    if (s1[i] == s2[j]) {
        return dp[i][j] = 1 + solve(i+1 , j+1 , n , m , s1 , s2, dp) ;
    }else {
        return dp[i][j] = max(solve(i+1 , j , n , m , s1 , s2, dp) , solve(i , j + 1 , n , m , s1 , s2, dp));
    }
}
int lcsLen(const string& s1 ,const string& s2) {
    int n = s1.length(); int m = s2.length();
    vector<vector<int>> dp(n , vector<int>(m , -1)) ;
    return solve(0 ,0 , n , m, s1 , s2 , dp) ;
}
int main() {
	string s1 = "tlkgregfna"; 
	string s2 = "tgkdmnogrkefn";
	// LCS
	cout << lcsLen(s1 , s2) << endl ;
}
```
