# KMP - LPS (Pattern Matching)

- Rather than check for the pattern from 0th character , from the start of every index in string s , {as in Brute force}
##  Intuition
- len = lps[len - 1] during LPS construction helps us reuse previous prefix matches to avoid recomputing.
- j = lps[j - 1] during search helps us skip unnecessary comparisons by jumping to the longest prefix that’s also a suffix.

## 🔍 Why KMP avoids restarting from scratch
Let’s say we’re searching "ababd" inside "ababcabcabababd" and we reach a mismatch at s[7] = 'x' vs pat[7] = 'b'

### Pattern: `"ababcab"`
**LPS Array**: `[0, 0, 1, 2, 0]`
`"ababcabcabababd"`
-  At index i = 12 the mismatch with j = 4 happen as from s we get `ababa` where from pattern I need `ababd`  as (a != d) so rather than revising i from the start (as in brute force we take ) j = lps[j-1] which is 2
-  as further the character `abd  in s` are match from pattern [2,m]  = `abd` hence the pattern is found

```cpp
// User function template for C++
class Solution {
  public:
    vector<int> get_lps(string& pat) {
        int m = pat.length(); 
        vector<int> lps(m , 0) ;
        
        int i = 1 ; int len = 0 ;
        while(i < m) {
            if (pat[i] == pat[len]) {
                len++ ;
                lps[i] = len ;
                i++ ;
            }else {
                if (len == 0 ){
                    lps[i] = 0 ;
                    i++ ;
                }else {
                    len = lps[len-1] ;
                }
            }
        }
        return lps ;
    }
    int search(string s, string pat) {
        if (s.length() < pat.length()) return 0 ;
        if (pat.length() == 0) return 1 ;
        int n = s.length();
        int m = pat.length();
        vector<int> lps = get_lps(pat) ;
        
        int j = 0 ;// to track for pat
        int i = 0 ;// traverse over s
        while (i < n) {
            if (s[i] == pat[j]) {
                i++ ; j++ ;
                if (j == m) return 1 ;
            }else {
                if (j > 0) {
                    j = lps[j-1] ;
                }else {
                    i++ ;
                }
            }
        }
        
        return 0 ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N + M)         |  O(M) from lps array , O(N) to travers to search for complete pattern using LPS |
| 🧠 SPACE |     O(M)       |LPS array  |

