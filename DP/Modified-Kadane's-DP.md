# MODIFIED KADANE'S ALGO 

- Try it :`https://www.algopath.ai/problems/0-1-hole`
- `Kadane` : used for max sub sum 
- But what if a ques is framed : 0-1 hole {we are free to remove a single element from any subarray if necessary and get the max subarray sum}
- Here removal of single element will obviously be the negative number causing the whole subarray contribute net < 0
- That is `Kadane's states that if the net contribution of any subarray is negative then discard it completely` , but keep in mind we can eliminate a single element if then removal of any ele give net positive then we can take the subarray

- Dp states : dp_with_removal[i] , dp_no_removal[i] {Upto ith element max_sum that can be obtained with or without the single ele removal}
- Without removal : dp_no_removal[i] = max(dp_no_removal[i-1] + a[i] , a[i])   `either start new subarray or continue with prev`
- Withremoval  : dp_with_removal[i] = max(dp_with_removal[i-1] + a[i] , dp_no_removal[i-1]) `either removed and any one in from prev indexes or remove the curr and take all from prev`

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n ;
    cin >> n ;
    vector<int> a(n) ;

    bool all_pos = true ;
    bool all_neg = true ;

    for (int i = 0 ; i < n ; i++) {
        cin >> a[i] ;
        if (a[i] >= 0) all_neg = false ;
        if (a[i] < 0) all_pos = false ;
    }

    if (all_neg) {
        cout << *max_element(a.begin() , a.end()) << endl ;
    }else if (all_pos){
        cout << accumulate(a.begin() , a.end() , 0) << endl ;
    }else {
        vector<int> dp_no_removal(n) ;
        vector<int> dp_with_removal(n) ;

        dp_no_removal[0] = a[0] ;
        dp_with_removal[0] = 0 ;

        int mx_sum = max(dp_no_removal[0] , dp_with_removal[0]) ;

        for (int i = 1 ; i < n ; i++) {
            dp_no_removal[i] = max(dp_no_removal[i-1] + a[i] , a[i]) ;
            dp_with_removal[i] = max(dp_with_removal[i-1] + a[i] ,dp_no_removal[i-1]) ;
            mx_sum = max({mx_sum , dp_no_removal[i] , dp_with_removal[i]});
        }
        cout << mx_sum << endl ;
    }

    return 0;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)        |     Single pass      |
| 🧠 SPACE |    O(N)        |     2 dp array       |
