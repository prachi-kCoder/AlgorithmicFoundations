# SPIRAL-ORDER-MATRIX-PRINTING

- This is simple traversal bound checking is neecessary to avoid out of boumd error and repetitive prints of the same element :

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& mat) {
        vector<int> res ;
        int n = mat.size();
        int m = mat[0].size();

        int r = 0 ; int c = 0 ;
        while (r < (n+1)/2 && c < (m+1)/2 ) {
            // L->R 
            for (int j = c ; j <= m-c-1 ;j++) {
                res.push_back(mat[r][j]) ;
            }
            // U -> D
            for (int i = r+1 ; i < n-r-1 ;i++) {
                res.push_back(mat[i][m-c-1]) ;
            }
            // R->L
            if (n-r-1 > r) {
                for (int j = m-c-1 ; j >= c ;j--) {
                    res.push_back(mat[n-r-1][j]) ;
                }
            }
            // D->U
            if ( c < m-c-1 ) {
                for (int i = n-r-2 ; i > r ;i--) {
                    res.push_back(mat[i][c]) ;
                }
            }
            r++ ; c++ ;
        }
        return res ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N x M)     |   Spiral traversal of matrix so each cell is visited once |
| 🧠 SPACE |    O(1)      |  No extra space take            |
