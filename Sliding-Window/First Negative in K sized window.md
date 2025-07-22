# SLIDING WINDOW 
### First negative in every window of size k 
```cpp
class Solution {
  public:
    vector<int> firstNegInt(vector<int>& arr, int k) {
        int n = arr.size();
        
        vector<int> res ;
        queue<int> q ;
        int i = 0 ;
        while (i < k-1) {
            if (arr[i] < 0) {
                q.push(i) ;
            }
            i++ ;
        }
        for ( i = k-1; i < n ; i++) {
            if (arr[i] < 0) {
                q.push(i) ;
            }
                if (i >= k) {
                    while (!q.empty() && q.front() < i-k+1) {
                        q.pop() ;
                    }
                }
                if (!q.empty()){
                    res.push_back(arr[q.front()]) ;
                }else {
                    res.push_back(0) ;
                }
        }
        return res ;
        
    }
};
```
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)         | Iterating over n sized array|
| 🧠 SPACE |     O(N)     |    Queue , Result array (n-k+1) size |

### OPTMISED APPROACH : 
#### TWO POINTER APPROACH  :(Keep track of negIdx) 
```cpp
 vector<int> firstNegInt(vector<int>& arr, int k) {
        int n = arr.size();
        
        vector<int> res ;
        
        int negIdx = 0;
        for ( int i = k-1 ; i < n ; i++ ) {
            while (negIdx < n && (negIdx < i - k + 1 || arr[negIdx] >= 0)) {
                negIdx++ ;
            }
            
            if (negIdx <= i && arr[negIdx] < 0) {
                res.push_back(arr[negIdx]) ;
            }else {
                res.push_back(0) ;
            }
        }
        
        return res ;
    }
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)         | Iterating over n-k+1 sized array|
| 🧠 SPACE |     O(1)     |    Pointer for negIdx used only |

