# CYCLE SORT 

### 🧪 When to Use Cyclic Sort
- Cycle Sort is not a general-purpose sorting algorithm. It works best under specific conditions:
- ✅ Ideal Conditions
- The array must contain distinct integers.
- All values should be in the range [1, n] or [0, n−1], where n is the size of the array.
- Each value has a unique correct position:
- 1) For `[1, n]`, value x should be at index `x - 1`.
- 2) For `[0, n−1]`, value x should be at index `x`.

### ❌ What It Can’t Handle
- Duplicates: It breaks the assumption that each value has a unique position.
- Out-of-bound values (e.g., < 0 or > n−1): These cause index errors or incorrect swaps.
- Negative numbers: Not supported unless you modify the logic.
- Unbounded ranges: If values don’t map directly to indices, the algorithm loses its efficiency and correctness.

### INTUITION :
- Each element ideally belongs at a specific index (e.g., value x should be at index x-1)

```cpp
#include <bits/stdc++.h>
using namespace std;
void cycleSort(vector<int>& nums) {
    int n = nums.size() ;
    int i = 0 ;
    while (i < nums.size()) {
        int rightPos = nums[i]-1 ;
        if (nums[i] != nums[rightPos]) {
            swap(nums[i] , nums[rightPos]) ;
        }else {
            i++ ;
        }
    }
}
int main() {
	vector<int> nums = {5,3,1,4,6,2} ;
	cycleSort(nums) ;
	for (int e : nums) {
	    cout << e << " ";
	}
	cout << endl ;
}

```
