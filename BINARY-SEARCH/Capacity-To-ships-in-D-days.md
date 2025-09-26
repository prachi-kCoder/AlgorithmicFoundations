# Capacty to ship within D-Days
Try Here : https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/
Or : https://www.geeksforgeeks.org/problems/capacity-to-ship-packages-within-d-days/1

```cpp
class Solution {
public:
    bool valid(int cap , int days , vector<int>& wts) {
        int n = wts.size();
        int d = 0 ; int i = 0 ;
        int shipped = 0 ;

        while (i < n) {
            shipped = wts[i] ;i++ ;
            while (i < n && shipped + wts[i] <= cap) {
                shipped += wts[i] ;
                i++ ;
            }
            d++ ;
            if (d > days) return false ;
        }    

        return true ;
    }
    int shipWithinDays(vector<int>& weights, int days) {
        int n = weights.size();
      
        
        int mx = *max_element(weights.begin(), weights.end());
        int total = accumulate(weights.begin(), weights.end(), 0);

        int low = mx  , high = total ;
        int min_cap = high ;
        while (low <= high) {
            int cap = low + (high - low)/2 ;
            if (valid(cap , days , weights)) {
                min_cap = cap ;
                high = cap-1 ;
            }else {
                low = cap+1 ;
            }
        }

        return min_cap ;
    }
};
```
