## HOUSE-ROBBER-2 
- Your turn : https://www.geeksforgeeks.org/problems/house-robber-ii/1
- To `prevent the 1st and last element to be taken in score as in cyclic movement both can't be considered together` :
- Solve range1 : `[0,n-2]`
- Solve range2 : `[1,n-1]`

```cpp
class Solution {
  public:
    int maxValue(vector<int>& arr) {
        int n = arr.size() ;
        
        vector<vector<int>> dp(n , vector<int>(2 , 0)) ;
        
        int prev_take = arr[0];
        int prev_skip = 0;
        for (int i = 1 ; i <= n-2 ; i++) {
            
            int c_skip = max(prev_skip , prev_take) ;
            int c_take = max(arr[i] + prev_skip , prev_take) ;
            prev_skip = c_skip ;    
            prev_take = c_take ;    
        }
        
        
        int f_take = prev_take ;
        int f_skip = prev_skip ;
        
        prev_take = arr[1] ;
        prev_skip = 0 ;
        
        for (int i = 2 ; i < n ; i++) {
            
            int c_skip = max(prev_skip , prev_take) ;
            int c_take = max(arr[i] + prev_skip , prev_take) ;
            prev_skip = c_skip ;    
            prev_take = c_take ; 
        }
        
        int s_take = prev_take ;
        int s_skip = prev_skip ;
        return max({f_take , f_skip , s_take , s_skip});
        
    }
};

```
