# MISSING NUMBER 
- CYCLE SORT
```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        // Cycle Sort 
        int n = nums.size();
        int i = 0 ;
        int res = -1 ;// where n lies ie missing as [0,n-1] in arr
        while (i < nums.size()) {
            int rightPos = nums[i]  ;// 0 at 0th index

            if (rightPos < nums.size() && nums[rightPos] != nums[i]) {
                swap(nums[rightPos] ,nums[i]) ;
            }else {
                i++ ;
            }
        }
        for (int i = nums.size()-1 ; i >= 0 ; i--) {
            if (nums[i] != i) {
                res = i ;
                break ;
            } ;
        }
        return res == -1 ? n : res ;
    }
};
```
## XORING APPROACH :

```cpp
int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int xorAll = 0;
        for (int i = 0; i < n ; i++) {
            xorAll ^= i ;
            xorAll ^= nums[i] ;
        }
        xorAll ^= n ;
        return xorAll ;
    }
```
