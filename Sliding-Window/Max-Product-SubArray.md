## Max-Product-SubArray

- Here we are just keeping the possibilities of getting curr_max , curr_min from neg and positive values both
- Thatis .
- `Curr_max` : May be maximised with curr_min computed so far if arr[i] -> -ve
- `Curr_min` : May be minimised with curr_max computed so far if arr[i] -> +ve
- {Curr_min : Is just to satify the possibility that if you get a -ve value at any ith index that curr_max can be maximised using `curr_min*arr[i]`}
```cpp
int maxProduct(vector<int> &arr) {
        
        int n = arr.size();
        if (n == 1) return arr[0] ;
        int curr_max = arr[0] , curr_min = arr[0] , res = arr[0] ;
        
        for (int i = 1 ; i < n ; i ++) {
            if (arr[i] == 0) {
                curr_max = 0 ;
                curr_min = 0 ;
                res = max(res , 0) ;
                continue ;
            }
            
            int prev_max = curr_max ;
            curr_max = max({arr[i] , curr_max*arr[i] , curr_min*arr[i]});
            curr_min = min({arr[i] , prev_max*arr[i] , curr_min*arr[i]});
            res = max(res , curr_max) ;
        }
        return res ;
    }
```
- O(N) time complexicity 
