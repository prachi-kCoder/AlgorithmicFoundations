# Koko-Eating-Bananas
- Try : https://leetcode.com/problems/koko-eating-bananas/
- k : piles size eaten / hr
- h : Total hrs
- n : Total hrs
- Get min k to complete eating the n piles in h hours

```cpp
bool possible(vector<int>& piles , ll k , int h) {
        int t = 0 ;
     
        
        for (int i = 0; i < piles.size() ;i++) {
            if (piles[i] <= k) {
                t++ ;
            }else {
                t += (piles[i] + k-1)/k ;
            }
            if (t > h) return false ;
        }
        return t <= h ;
    }
    int minEatingSpeed(vector<int>& piles, int h) {
        int n = piles.size();
        sort(piles.begin() , piles.end());
        reverse(piles.begin() , piles.end());

        ll mx = *max_element(piles.begin(), piles.end());

        ll low = 1 , high = 1LL*n*mx ;
        ll min_k = mx ;
        while (low <= high) { // minimise k
            ll k = low + (high-low)/2 ;
            if (possible(piles , k , h )) {
                min_k = k ;
                high = k-1 ;
            }else {
                low = k+1 ;
            }
        }

        return min_k ;
    }
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |      O(Nlog(mx_k))      |      check for N-elements validity for & binary search over the [1,mx_k] range so O(mx_k) * N {elements time cal for all k}     |
| 🧠 SPACE |    O(1)        |      No extra space taken       |
