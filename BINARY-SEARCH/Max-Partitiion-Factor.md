## Max-Partitiion-Factor

- YOUR TURN : https://leetcode.com/problems/maximum-partition-factor/

- INTUITION OF `BINARY SEARCH`  comes from maximising the `{ min(manhatten dist) = Pf}` where pf->partition factor
- Whenever we need such an answer with right partition and need to maximise it  use B_search
- Now `2-sat` is applied here as we need to categories the points in 2 Different gps as is can manhatten dist is low so they should not be in same gouup otherwise min{intra manhatten distances of gps-points}- > less
- GPS  : A[0 - n-1] , B[n ,2n-1 ] these gps if possible then a partition for a manhatten distnat is possible !

```cpp
class DSU {
public :
    vector<int> par , ranking ;
    DSU(int n) {
        par.resize(n+1);
        ranking.resize(n+1 , 0);
        for (int i = 0; i <= n ; i++) par[i] = i ;
    }
    int find(int x) {
        if (par[x] == x) return x ;
        return par[x] = find(par[x]) ;
    }
    bool unify(int u , int v) {
        int pu = find(u); int pv = find(v);
        if (pu == pv) return false ;
        if (ranking[pu] > ranking[pv]) {
            par[pv] = pu ;
        } else if (ranking[pv] > ranking[pu]) {
            par[pu] = pv ;
        } else {
            par[pu] = pv ;
            ranking[pv]++ ;
        }
        return true ;
    }
};
class Solution {
public:
    int n ;
    int manh(vector<int>& a , vector<int>& b) {
        return abs(a[0] - b[0]) + abs(a[1] - b[1]) ;
    }
    bool valid(int dist , vector<vector<int>>& points ) {
        DSU dsu(2*n) ;

        for (int i = 0 ; i < n; i++) {
            for (int j = i+1 ; j < n ; j++ ) {
                int d = manh(points[i] , points[j]) ;
                if (d < dist) {
                    dsu.unify(i , j+n);  // separate in 2 different : gp of n
                    dsu.unify(i + n , j); // separate in 2 different : gp of n
                }
            }
        }
        for (int i = 0 ; i < n ; i++) {
            if (dsu.find(i) == dsu.find(i+n)) return false ;
        }
        return true ;
    }
    int maxPartitionFactor(vector<vector<int>>& points) {
        n = points.size() ;
        if (n == 2) return 0 ; 
        
        int low = 0 ;
        int high = 0 ;
        for (int i = 0; i < n ; i++) {
            for (int j = i+1 ; j < n ; j++) {
                high = max(high ,manh(points[i] , points[j])) ;
            }
        }
        int ans = 0 ;
        while (low <= high) {
            int mid = low + (high-low)/2 ;
            if (valid(mid , points)) {
                ans = mid ;
                low = mid + 1 ;
            }else {
                high = mid - 1 ;
            }
        }
        return ans ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N x N x log(D) ) | D is the maximum Manhattan distance among all point pairs. For each binary search step (log D), we check feasibility by iterating over all pairs (O(N²)) and applying DSU operations.       |
| 🧠 SPACE |    O(N)        | Par , Size , Ranking |
