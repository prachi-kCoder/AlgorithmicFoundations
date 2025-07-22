# Count occurence of anagrapms 

```cpp
// User function template for C++
class Solution {
  public:
    int search(string &pat, string &txt) {
        int m = pat.length();
        int n = txt.length();
        int res = 0 ;
        vector<int> freq(26,0) , window(26,0) ;
        
        for (int i = 0; i < m ; i++ ) freq[pat[i]-'a']++ ;
        
        
        for (int i = 0 ; i < m ; i++) {
            window[txt[i]-'a']++ ;
        }
        if (freq == window) res++;
        
        for (int i = m ; i < n ; i++) {
            window[txt[i]-'a']++ ;
            window[txt[i-m]-'a']-- ;
            if (freq == window) res++;
        }
        return res ;
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N + M)    |  Traversal m , n length    |
| 🧠 SPACE |  Freq , window        |   2 freq arrays to match char occurence |
