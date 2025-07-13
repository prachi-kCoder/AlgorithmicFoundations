# ROTTING ORANGES 
```cpp
class Solution {
public:
    constexpr static int dx[] = {-1 , 0 , 1 , 0 } ;
    constexpr static int dy[] = { 0 , 1 , 0 , -1} ;
    int orangesRotting(vector<vector<int>>& grid) {
        int n = grid.size() ; int m = grid[0].size();
        bitset<10*100> mask(0) ;
        queue<pair<int,int>> q ;

        for (int i = 0; i < n ; i++) {
            for (int j = 0; j < m ; j++) {
                if ( grid[i][j] == 2 ) {
                    q.push({i,j});
                } else if (grid[i][j] == 1) {
                    // freshSet.insert(100*i + j);
                    mask.set(100*i + j);
                }
            }
        }
        int t = 0 ;
        while (!q.empty()) {
            int sz = q.size();
            
            bool nxt = false ;
            for (int l = 0 ; l < sz ; l++)  {
                auto p = q.front(); q.pop();
                int i = p.first  , j = p.second ;
                for (int k = 0 ; k < 4 ; k++) {
                    int nx = i + dx[k] , ny = j + dy[k] ;

                    if (nx >= 0 && nx < n && ny >= 0 && ny < m && grid[nx][ny] == 1) {
                        nxt = true ;
                        grid[nx][ny] = 2 ;
                        int key = nx*100 + ny ;
                        // if (freshSet.find(key) != freshSet.end()) {
                        mask.reset(key);
                        // }
                        q.push({nx, ny});
                    }
                }
            }
            if (nxt) t++ ;
        }
        if (mask.count() > 0) return -1 ;
        return t ;
    }
};
```

# 🧮 Complexity Analysis
| METRIC   |  COMPLEXICTY    |  HOW ?  | 
| 🌀 TIME     |  O(n*m)   | Grid Traversal  + Level wise enque/deque |
| 📦SPACE    |  O(100*10 + 10) + O(n*m) | BITMASK + Queue |
