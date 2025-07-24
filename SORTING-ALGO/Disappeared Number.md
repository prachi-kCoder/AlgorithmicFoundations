# DISAPPEARED NUMBERS
- CYCLE SORT (Put the elements at their right position)

```cpp
vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> mis ;
        int n = nums.size();

        int i = 0; 
        while (i < n) {
            int rightPos = nums[i]-1 ;
            if (nums[rightPos] != nums[i]){
                swap(nums[rightPos] , nums[i]);
            }else {
                i++;
            }
        }
        for (int i = 0; i < n ; i++) {
            if (nums[i] != i+1) {
                mis.push_back(i+1) ;
            }
        }
        return mis ;
    }
```
