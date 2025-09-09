# Sliding-window-mex

- Keep in mind of a window if size `k` the maximum mex could be `k` {when 0-(k-1) all present}
- Keep the freq of element of value upto k and use set to keep track of the smallest missing element in the curr window {using set}
- take the smallest element missing and record as `mex`
  
```cpp
#include <bits/stdc++.h>

using namespace std;
int main() {
    int n , k ;
    cin >> n >> k ;
    set<int> missing ;
    vector<int> a(n) ;
    
    for (int i = 0; i < n; i++) {
        cin >> a[i] ;
    }
    for (int i = 0; i <= k ;i++) missing.insert(i) ;
    vector<int> freq(k+2, 0) ;

    for (int i = 0 ; i <= k-1 ; i++){
        if (a[i] <= k) {
            freq[a[i]]++ ;
            if (freq[a[i]] == 1) missing.erase(a[i]) ;// if present 
        }
    }

    cout << *missing.begin() << " ";
    for (int i = k  ; i < n ; i++) {
        if (a[i] <= k) {
            freq[a[i]]++ ;
            if (freq[a[i]] == 1) missing.erase(a[i]) ;
        }
        if (a[i-k] <= k) {
            freq[a[i-k]]-- ;
            if (freq[a[i-k]] == 0 ) {
                missing.insert(a[i-k]) ;
            }
        }
        cout << *missing.begin() << " " ;
    }
    cout << endl ;
    return 0;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O (N logK)     | set keep track of smallest missing in range [0,k] so K elements can be inserted and popped out of set|
| 🧠 SPACE |     O (K)       | Freq array {k+2 size} , Set of missing [0,k]           |
