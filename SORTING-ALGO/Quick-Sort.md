# QUICK SORT

- Recursive function based on Pivot & Partition technique
- Assuming last ele as pivot , then take all ele <= pivot on left & ele > pivot on right , then call quickSort for left Part and rightPart

```cpp
#include <bits/stdc++.h>
using namespace std;
int partition(vector<int>& nums, int si , int ei) {
    int i = si - 1 ;
    int pivot = nums[ei] ;
    for (int j = si ; j < ei ; j++) {
        if (nums[j] <= pivot) {
            i++ ;
            swap(nums[j] , nums[i]) ;
        }
    }
    i++;
    swap(nums[i] , nums[ei]) ;

    return i ;
}
void quickSort(vector<int>& nums , int si, int ei) {
    if (si >= ei) return ;
    int pIdx = partition(nums, si, ei) ;
    quickSort(nums, si , pIdx-1) ;
    quickSort(nums, pIdx + 1 , ei) ;
}
int main() {
	vector<int> nums = {78,3,2,70,-90,-4,33};
	int n = nums.size();
	quickSort(nums , 0 , n-1) ;
	for (int ele : nums) {
	    cout << ele << " " ;
	}
	cout << endl ;
}
```

- Unstable Algorithm as the relative order of equal element can be lost while making comparisions with pivot element unlike Merge Sort (which is  stable)
  
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(NlogN) {In Avg & Best Case} , **O(N^2)**  {Worst Case}     |  Worst Case :{One-Sided partitions eg already sorted array with bad pivot}          |
| 🧠 SPACE |    O(logN)    | Recursion Stack   |

