# MERGE-SORT
```cpp
#include <bits/stdc++.h>
using namespace std;
void merge(vector<int>& nums , int si , int ei , int mid) {
    int len = ei - si + 1 ;
    vector<int> merged(len) ;
    int k = 0 ;
    int i = si ; int j = mid + 1 ;
    while (i <= mid && j <= ei) {
        if (nums[i] <= nums[j]) {
            merged[k++] =  nums[i++] ;
        }else {
            merged[k++] =  nums[j++] ;
        }
    }
    while (i <= mid) {
        merged[k++] =  nums[i++] ;
    }
    while (j <= ei) {
        merged[k++] =  nums[j++] ;
    }
    
    for (int t = 0 ; t < len ; t++ ) {
        nums[t + si] = merged[t] ;
    }
}
void mergeSort(vector<int>& nums, int si , int ei) {
    if (si >= ei) return  ;
    
    int mid = si + (ei - si)/2 ; // or can do (si + ei) >> 1
    mergeSort(nums , si , mid) ;
    mergeSort(nums , mid + 1 , ei) ;
    
    merge(nums , si , ei , mid );
}
int main() {
	vector<int> nums = {500,1000,10,-88,-22,2,8,9};
	int n = nums.size() ;
	mergeSort(nums, 0, n-1 ) ;
	for (int ele : nums) {
	    cout << ele <<" " ;
	}
	cout << '\n' ;
	return 0;
}
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(nlogn)    |   First recursion calls for logn depth , then merging all elements = len of nums in each call |
| 🧠 SPACE |   O(N + logn) = O(N)     |   Recursion Stack + the temp array (but it is freed as soon as merging is done) |

