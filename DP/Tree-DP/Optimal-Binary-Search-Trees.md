## Tree-DP

- Although binary search : searching is Optimal with O(logN) but in case we want the even faster searchin for those keys specially which are frequently accessed
- Move freq of search -> Near to root of Binary Seach Trees
- But keeping it as BST {ordered!}
- Total bst possible = C(2N , N) / (N+1) {as we make by catalan ques}
- among these if we choose the best BST : with the key having most freq element near to the root -> MOST EFFICIENT
- Hence we are need to consider which one to make root node

- Eg A {30} , B{1}, C {20} here nodes with freq of access
- BEST BST will be to make A {root}
- & C as right of A and
- B as left of C

OR  A {3} , B{100}, C {20}  then A {left} , B {root} , C{right} will be most efficient .

## naive o(n3)
```cpp
#include <bits/stdc++.h>
using namespace std;
int minCost(vector<int> &keys, vector<int> &freq) {

        int n = keys.size();

        // dp to store cost of arrangements of nodes from 

        // dp[i,j] = dp[i,k] + dp[k+1,j] + sumfofreq{i,j}

        vector<vector<int>> dp(n , vector<int>(n , INT_MAX)) ;

        vector<int> pre(n, 0LL) ;

        

        for (int i = 0 ; i < n ; i++) dp[i][i] = freq[i] ;

        pre[0] = freq[0] ;

        for (int i = 1 ; i < n ; i++) {

            pre[i] = pre[i-1] + freq[i] ;

        }

        

        for ( int len = 2 ; len <= n ; len++ ){

            for (int i = 0 ; i <= n-len ; i++) {

                int j = i + len - 1 ;

                dp[i][j] = INT_MAX ;

                int range_freq = pre[j] - ( i > 0  ? pre[i-1] : 0 ) ;

                for (int k = i ; k <= j ; k++) {

                    int left_cost = (k > i ?  dp[i][k-1] : 0 ) ;

                    int right_cost = (k < j ?  dp[k+1][j] : 0) ;

                    dp[i][j] = min(dp[i][j] , left_cost + right_cost + range_freq ) ;

                }

            }

        }  
        return dp[0][n-1] ;

    }
int main() {
	vector<int> keys = {10, 12, 20} ;
	vector<int> freq = {34, 8, 50};
	cout << minCost(keys, freq) << endl ;


    return 0;
}

```
- Kunth optimisation  {Keep track of the root of smaller ranges and then lower down the complete
- range[i,j] -> [L,R] where L = root[i][j-1] , R = root[i+1][j]}
## O(N^2) 

-> after telescoping the sum of iterations performed

```cpp
class Solution {
  public:
    int minCost(vector<int> &keys, vector<int> &freq) {
        int n = keys.size();
        // dp to store cost of arrangements of nodes from 
        // dp[i,j] = dp[i,k] + dp[k+1,j] + sumfofreq{i,j}
        vector<vector<int>> dp(n , vector<int>(n , INT_MAX)) ;
        vector<vector<int>> root(n , vector<int>(n , 0)) ;
        vector<int> pre(n, 0LL) ;
        
        for (int i = 0 ; i < n ; i++) {
            dp[i][i] = freq[i] ;
            root[i][i] = i ;
        }
        pre[0] = freq[0] ;
        for (int i = 1 ; i < n ; i++) {
            pre[i] = pre[i-1] + freq[i] ;
        }
        
        for ( int len = 2 ; len <= n ; len++ ){
            for (int i = 0 ; i <= n-len ; i++) {
                int j = i + len - 1 ;
                
                int range_freq = pre[j] - ( i > 0  ? pre[i-1] : 0 ) ;
                int L = root[i][j-1] ;
                int R = root[i+1][j] ;
                
                for (int k = L ; k <= R ; k++) {
                    int left_cost = (k > i ?  dp[i][k-1] : 0 ) ;
                    int right_cost = (k < j ?  dp[k+1][j] : 0) ;
                    int curr = range_freq + left_cost + right_cost ;
                    if (curr < dp[i][j]) {
                        dp[i][j] = curr ;
                        root[i][j] = k ;
                    }
                }
            }
        }
        
        return dp[0][n-1] ;
    }
};
```
