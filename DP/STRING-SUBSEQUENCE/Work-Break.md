# Word-Break

```cpp
// User function template for C++

class Solution {
  public:
    // A : given string to search
    // B : vector of available strings
        vector<int> dp ;
    bool check(string A , int si , set<string>& word_set) {
        if (si >= A.length()|| word_set.find(A.substr(si)) != word_set.end()) {
            return true ;
        }
        if (dp[si] != -1) return (dp[si] == 1) ;
        for (int i = si ; i < A.length() ;i++) {
            string f = A.substr(si , i - si + 1) ;
            if (word_set.find(f) != word_set.end()) {
                if (check(A, i+1 , word_set)) return dp[si] = true ;
            }
        }
        
        return dp[si] = 0 ;
    }
    int wordBreak(string A, vector<string> &B) {
        // code here
        int n = A.length();
        dp.resize(n, -1 ) ;
        set<string> word_set(B.begin() , B.end()) ;
        return check(A ,0, word_set) ;
    }
};
```
