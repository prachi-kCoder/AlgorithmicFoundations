# Sudoku-Problem

- Here sudoku given with partial entries solve it so
- Check for row , col , box
- Interestingly `row = [0-8]` , `col[0-8]`, `box[0-8]`
- Take helf or bitmask to keep track of what number are used in row/col/box
- Ie at every ith index in row/col/box : Take mask `00000000`  as soon as any num [1-9] found to be used or , on recursion use vis it as per `0-indexing of [0-8]` and then go further

- Sometimes it always hard to decide now if we start a 0th row and 0th col, then do we need to track the row covered so far and if col = 9 then switch to new col
- but this is solve by accessing cells `[0-80]` ie 81 cells so keep on marking them and and retreive the ith and jth col from the cell num on the cell


```cpp
class Solution {
public:
    int n ;
    vector<int> row ;
    vector<int> col ;
    vector<int> box ;
    bool solve(int cell , vector<vector<char>>& board) {
        if (cell >= 81) return true;
        int i = cell/9 ; int j = cell%9 ;
        if (board[i][j] != '.') return solve(cell+1 , board) ;

        int bn = (i/3)*3 + (j/3) ;
        for ( int d = 0 ; d < 9 ; d++ ) {
            if (row[i]&(1<<d)) continue ;
            if (col[j]&(1<<d)) continue ;
            if (box[bn]&(1<<d)) continue ;
            row[i] = (row[i]|(1<<d)) ;
            col[j] = (col[j]|(1<<d)) ;
            box[bn] = (box[bn]|(1<<d)) ;
            board[i][j] = (char)((d+1) + '0') ;

            if (solve(cell+1 , board)) return true ;
            board[i][j] = '.' ;
            row[i] = (row[i]^(1<<d)) ;
            col[j] = (col[j]^(1<<d)) ;
            box[bn] = (box[bn]^(1<<d)) ;
        }

        return false ;
    }
    void solveSudoku(vector<vector<char>>& board) {
        n = board.size();
        // mark already given cells 
        row.resize(n,0);
        col.resize(n,0);
        box.resize(n,0);
        for (int i = 0; i < n ; i++) {
            for (int j = 0; j < n ; j++) {
                if (board[i][j] != '.') {
                    int bn = (i/3)*3 + (j/3) ;
                    int val = (board[i][j] - '0') ;
                    val-- ;
                    row[i] = (row[i]|(1<<val)) ;
                    col[j] = (col[j]|(1<<val)) ;
                    box[bn] = (box[bn]|(1<<val));
                }
            }
        }
        solve( 0 , board) ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |  𝑂(9^𝑘) with no pruning , but with row,col,box checking it will be much lower    |  Worst case with no pruning take O(9^k) where k are empty cells , because at every cell O(9) possibilities so total = O(9^k)         |
| 🧠 SPACE |   3*O(9) = O(1)          |    # bitmasking array         |
