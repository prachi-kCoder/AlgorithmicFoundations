# LEVEL BACKTRACKING 

- Often used to get all possible `UNIQUE` permutations of a string / array
- We look for `start` always
  
- Q1) Get all permutations unique permutations of arr of len = arr.size()
- Here `start` was not necessary as v was shrinking !
-  ✅ Unique permutations via level-based backtracking
-  🔁 Erase + insert to simulate element usage
- ⚠️ Skip duplicates using sorted input and i > 0 check

```cpp
#include <bits/stdc++.h>
using namespace std;
// Level BackTracking for Unique Permutation for  arr<int> for same n size 
void print(vector<int>& v) {
    for (int e : v) {
        cout << e << " " ;
    }
    cout << endl ;
}
void helper(vector<int>& curr, vector<int>& v) {
    if (v.empty()) {
        print(curr);
        return;
    }
    for (int i = 0; i < v.size(); ++i) {
        if (i > 0 && v[i] == v[i - 1]) continue; // skip duplicates
        curr.push_back(v[i]);
        int ele = v[i];
        v.erase(v.begin() + i);
        helper(curr, v);
        curr.pop_back();
        v.insert(v.begin() + i, ele);
    }
}
void permute_arr(vector<int>& v) {
    int n = v.size();
    // get all same element together
    sort(v.begin() , v.end()) ;
    vector<int> curr ;
    helper(curr, v ) ;
}
int main() {
    vector<int> v = {2,2,3,1,1};
    permute_arr(v) ;
}
```
- here start is not so significant 
# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N! * N)    |   All N! permutations of N si        |
| 🧠 SPACE |   O(N)         |   Vector for the permutations         |

- Q2) Get all str permutations unique permutations of s of len = s.length()

```cpp
class Solution {
  public:
    void permute(string& ns , string& s , vector<string>& v) {
        if (s.empty()) {
            v.push_back(ns) ;
            return ;
        }
        int n = s.length() ;
       
        for (int i = 0 ; i < n ; i++) {
            if (i > 0 && s[i] == s[i-1]) continue ; 
            ns.push_back(s[i]) ;
            string left = s.substr(0 , i) + s.substr(i+1) ;
            permute( ns , left , v) ;
            ns.pop_back() ;
        }
    }
    vector<string> findPermutation(string &s) {
        vector<string> v;
        sort(s.begin() , s.end()) ; 
        // to get same character together!
        string ns = "" ;
        permute(ns , s , v);
        return v ;
    }
};

```


# BUT NOW LET'S USE `start` 
- 
