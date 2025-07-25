# COUNT- SORT :
- **Only for when the element are in non-megative ranges , and upto a fixed mx values (reachable)!**
```cpp
#include <bits/stdc++.h>
using namespace std;
void countSort(vector<int>& nums) {
    int n = nums.size();
    int mx = *max_element(nums.begin() , nums.end()) ;
    vector<int> f(mx + 1) ;
    for (int e : nums) f[e]++ ;
    int j = 0, i = 0 ; 
    
    while (i <= mx){
        while (i <= mx && f[i] == 0) i++ ;
        if (i <= mx) {
            nums[j++] = i ;
            f[i]--;
        }
        if(f[i] == 0) i++ ;
    }
}
int main() {
	vector<int> nums = {4,8,7,3,7,1,2,2,16,9};
	int n = nums.size() ;
	countSort(nums) ;
	for (int e : nums) {
	    cout << e << " " ;
	}
	cout << endl ;
}

```

# 🔍 Complexity Analysis


| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n+k)         |  Counting frequencies takes O(n), rebuilding sorted output takes up to O(k) where k :is max element value.         |
| 🧠 SPACE |   O(k)       |   Freq array upto k (mx element)       |
