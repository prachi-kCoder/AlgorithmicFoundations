# TRAPPING RAIN WATER :
## Approach 1 :
- Space Complexicity O(N) , Time Complexcity O(N)

```cpp
class Solution {
  public:
    int maxWater(vector<int> &arr) {
        int n = arr.size() ;
        if (n <= 1) return 0 ;
        //  2Pointer Approach 
        // LeftMx Ht - RightMax Ht
        vector<int> rmx(n ) ;
        rmx[n-1] = arr[n-1] ;
        for (int i = n-2 ; i >= 0  ; i--) {
            rmx[i] = max(rmx[i+1] , arr[i]) ;
        }
        int lmx = arr[0] ;
        int total = 0;
        for (int i = 1 ; i < n ; i++) {
            total += max(0 , min(lmx , rmx[i]) - arr[i] ) ;
            lmx = max( arr[i] , lmx ) ;
        }
        
        return total ;
    }
};
```
## APPROACH : 2 POINTER 
- Space Complexicity : O(1)
- Time Complexicity : O(N)

```cpp
class Solution {
  public:
    int maxWater(vector<int> &arr) {
        int n = arr.size() ;
        if (n <= 1) return 0 ;
        //  2Pointer Approach 
        int l = 0 , r = n-1 ;
        int lmx = 0 , rmx = n-1 ;// index
        int total =  0 ;
        while (l < r) {
            if (arr[l] <= arr[r]) {
                if (arr[lmx] < arr[l]) lmx = l ;
                total += arr[lmx] - arr[l] ;
                l++ ;
            }else {
                if (arr[rmx] < arr[r]) rmx = r ;
                total += arr[rmx] - arr[r] ;
                r-- ;
            }
        }
        
        return total ;
    }
};
```

## APPROACH 3 : Stack - Approach 
```cpp
int maxWater(vector<int> &arr) {
        
        int n = arr.size();
        stack<int> stk ;
        int total = 0 ;
        
        for (int i = 0; i < n ; i++) {
            while (!stk.empty() && arr[i] > arr[stk.top()]) {
                int btmIdx = stk.top();
                stk.pop();
                if (stk.empty()) break ;
                
                int left = stk.top();
                int width = i - left - 1 ;
                int ht = min(arr[i] , arr[left]) - arr[btmIdx] ;
                if (ht > 0) {
                    total += width*ht ;
                }
            }
            stk.push()
        }

        return total ;
        
    }
```


# 🔍 Complexity Analysis
### STtack approach
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)        |  Each bar/arr[i] is pushed & popped at most once in stack and traversal of array    |
| 🧠 SPACE |  O(N)          | Stack used       |
