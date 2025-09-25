## ALLOCATE MIN -PAGES.MD

- Solve here : https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1

```cpp
class Solution {
  public:
    bool possible(int mx_page , vector<int>& arr, int k) {
        int n = arr.size();
        int c = 1 ;
        
        int page = 0 ;
        for (int i = 0 ; i < n ; i++) {
            if (page + arr[i] <= mx_page) {
                page += arr[i] ;
            }else {
                if (c >= k) return false ;
                page = arr[i] ;
                c++ ;
            }
        }
      
        return true;
    }
    int findPages(vector<int> &arr, int k) {
        int n = arr.size();
        if (n < k) return -1 ;
        
        int low = *max_element(arr.begin() , arr.end()) ;
        int high = accumulate(arr.begin() , arr.end() , 0) ;
        int res = high ;
        
        while (low <= high) {
            int mid = low + (high-low)/2 ;
            if ( possible(mid , arr,  k) ) {
                res = mid ;
                high = mid-1 ;
            }else {
                low = mid+1 ;
            }
        }
        
        return res ;
        
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N*log(total-mx))  |  The binary search range is `[max(arr), sum(arr)]`, so the number of iterations is log(sum(arr) - max(arr)) , check the validity for k students with N books |
| 🧠 SPACE |    O(1)        |    Constant space        |
