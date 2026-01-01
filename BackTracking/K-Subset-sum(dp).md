# K-Subset-sum(dp)
# DO : https://www.geeksforgeeks.org/problems/partition-array-to-k-subsets/1
- BRUTE FORCE ie keep a vector<int> subsets and try adding all ele of arr in any of these while backtracking -> TLE as O(k^n) not feasible of k , n upto [1,10]
-  OPTIMISED DP + BITMASK
-  TargetVal of each subset = Sum of all val / k ;
- dp[mask] = sub of elements of mask mod target
- Result is dp[full_mask] == 0 , ie if a set of all element of array used to make this and their sum was successfully was = target_sum so mod of it = 0 ,
- As all elements used & giving `subset_sum = target` , ie `subset_sum = total/k` => `k*subset_sum = total` ie
- all elements we successfully divided in k subsets

### TC =  O(n*2^n)

```cpp
bool isKPartitionPossible(vector<int> &arr, int k) {
        // Your code here
        int n = arr.size();
        int sum = accumulate(arr.begin() , arr.end() , 0) ;
        if (sum%k != 0) return false ;
        
        vector<int> dp((1<<n) , -1) ;
        dp[0] = 0 ;// element with 0 total are initially 0 
        
        int target = sum/k ;
        for (int mask = 0; mask < (1<<n) ; mask++) {
            if (dp[mask] == -1) continue ;
            
            for (int i = 0 ; i < n ; i++) {
                // subset should not have this element 
                if (!(mask & (1<<i))) {
                    if (dp[mask] + arr[i] <= target) {
                        dp[mask | (1<<i)] = (dp[mask] + arr[i])%target ;// keep the sum of ele 
                    }
                }
            }
        }
        
        return dp[(1 << n)-1] == 0 ; // all value subset should sum upto = target so mod = 0
    }
```
