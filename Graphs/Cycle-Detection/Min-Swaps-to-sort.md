# MIN - SWAPS TO SORT 

### on the first try sometime it does seems like an cycle detection question
- Problem : given unsorted array in min swaps possible
- Where `CYCLE-DETECTION`
- Look think if you got a larger elemnet on smaller idx then you can swap it with another smaller / larger value
- Actually our focus is to check what are `miss-placed elements` , Get them identified by sorted keeping their original idx in given array , observer if not place rightly
- For miss-placed : If any element e should be on idx i but placed on idx j them check who belongs to j originally , some e2 at jth index then e2 should be at jth index but in given array what position does it occupies ? then keep checking until you get any element rightly placed ie the cycle
- But wait what if they get entangled in cycle pointing to each other , then we need `vis[idx]` to mark any misplaced ele whether detected or not
- As soon as all nodes are covered , the `swaps = cycle len - 1`  as eg for cycle of 4 element 1->2->3->4->1  here size = 4 {as 1 is already vis} so the swaps made will be b/w a pair so cycle_size-1


```cpp
 int minSwaps(vector<int>& arr) {
        int n = arr.size();
        vector<pair<int,int>> v ;
        
        for (int i = 0 ; i < n ; i++) {
            v.push_back({arr[i] , i});
        }
        sort(v.begin() , v.end()) ;
        vector<bool> vis(n , false) ;
        
        int swaps = 0 ;
        
        for (int i = 0 ; i < n ; i++ ) {
            if ( v[i].second != i ) {
                int cycle_len = 0 , j = i ;
                
                while (!vis[j]) {
                    cycle_len++ ;
                    vis[j] = true ;
                    j = v[j].second ;
                }
                swaps += max(0,cycle_len - 1) ;
            }
        }
        
        return swaps ;
    }
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N x logN) | Sorting of `n` pairs |
| 🧠 SPACE |    O(N)        |       All pairs       |
