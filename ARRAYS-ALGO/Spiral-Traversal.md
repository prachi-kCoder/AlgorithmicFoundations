# Spiral-Traversal
#### 🧭 Why Right Move for Odd Rows (top == btm)
- When top == btm, you're down to a single row. In spiral traversal, this typically happens at the end when the matrix has an odd number of rows. At this point:
- You only want to move right across that row.
- You don’t want to go left again because that would repeat elements or go out of bounds. 
- So your condition if (top <= btm) allows the rightward move when top == btm, but not for the left movement 

#### 📐 Why Down Move for Odd Columns (left == right)
- Similarly, when left == right, you're down to a single column. This happens when the matrix has an odd number of columns. At this point:
- You only want to move down that column.
- You don’t want to go up again, which would either repeat or access invalid indices.
- So your condition if (left <= right) allows the downward move when left == right.

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n , m ;
    cin >> n >> m ;
    vector<vector<int>> mat(n , vector<int>(m)) ;
    for (int i = 0 ; i < n ; i++ ) {
        for (int j = 0 ; j < m ; j++ ) {
            cin >> mat[i][j] ;
        }
    }
    // top row , btm row , left col , right col
    int top = 0 , btm = n-1 , left = 0 , right = m-1 ;
    while (top <= btm || left <= right) {
// Equality only for Right & Down move 

        if (top <= btm) { 
            // [left col to right col]
            for (int j = left  ; j <= right ; j++) {
                cout << mat[top][j] << " " ;
            }
        }
        if (left <= right) {
            //Down :[top+1 row  to btm row] 
            for (int i = top+1  ; i <= btm ; i++) {
                cout << mat[i][right] << " " ;
            }
        }
        if (top < btm) { 
            // [left col to right col]
            for (int j = right-1  ; j >= left ; j--) {
                cout << mat[btm][j] << " " ;
            }
        }
        if (left < right) { 
            // [down to up]
            for (int i = btm-1 ; i >= top+1 ; i-- ) {
                cout << mat[i][left] << " " ;
            }
        }
        top++ ; btm--;
        left++ ; right-- ;
    }
    return 0;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*N)   | All cells of mat are traversed |
| 🧠 SPACE |    O(1)        |        No extra space    |
