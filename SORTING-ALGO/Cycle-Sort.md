# CYCLE SORT 

### 🧪 When to Use Cyclic Sort
- Cyclic Sort shines when:
  - You’re given an array of size n with elements from 1 to n or 0 to n & Elements are distinct or bounded within a known range
  - You need to find missing numbers, duplicates, or misplaced elements
  - You want O(n) time and O(1) space

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
