# RAT MAZE 
- POINTS TO KEEP IN MIND
- Do mark the visited cells to not to visit them in the same path
- Keep track of path
- Grid  V/S Cartesian Cell confusion : While we go in directions :
  
           - vector<int> dr = {0, 1, 0, -1};      // L D R U (Clockwise)
           - vector<int> dc = {-1, 0, 1, 0};
           - vector<char> dir = {'L', 'D', 'R', 'U'};
  Here in this i have seen a confusion of directions as in grid row , col,  cartesian plane (y , x) as row changes y value changes , col changes x  (Donot mismatch b/w these)
  Eg (0,1) ie same row next col in GRID  : ie "Right"
      (0,1) in Cartesian plane  +0 to x , +1 to y => Feels like Up here
-  Follow grid convention , in in Clockwise for better uniformity and order
- Sort at the end to get the right Lexo ordered seq of paths 
 
```cpp
class Solution {
  public:
  // cw
    vector<int> dr = {0, 1, 0, -1};      // L D R U
    vector<int> dc = {-1, 0, 1, 0};
    vector<char> dir = {'L', 'D', 'R', 'U'};
    int n  ;
    void solve(int i , int j , vector<vector<int>>& maze ,const string& path, vector<string>& res) {
        if (i == n-1 && j == n-1) {
            res.push_back(path) ;
            return ;
        }
        if (i >= n || j >= n ) return  ;
        maze[i][j] = 2 ; // vis
        for (int k = 0; k < 4 ; k++) {
            int nx = i + dr[k] ; int ny = j + dc[k] ;
            if (nx >= 0 && ny >= 0 && nx < n && ny <n && maze[nx][ny] == 1 ) {
                solve(nx , ny , maze ,  path +  dir[k]  , res) ;
            }
        }
        maze[i][j] = 1 ; // retrack
        
    }
    vector<string> ratInMaze(vector<vector<int>>& maze) {
       n = maze.size();
       
       vector<string> res ;
       if(maze[0][0] == 0 || maze[n-1][n-1] == 0) return res ;
       
       string path = "" ;
       solve(0 , 0, maze ,path, res) ;
      sort(res.begin() , res.end()) ;
       return res ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(4^(N*N))   |  For all cell , all 4 directions , all adjcent paths are traversed, However, efficient backtracking with visited tracking prunes the search space significantly.       |
| 🧠 SPACE |   O(N*N)   |   Recursion Stack: In a recursive backtracking solution (like DFS), the maximum depth of the recursion stack can be N*N in the worst case. This happens when the path from the source to the destination involves traversing almost all cells in the grid sequentially without revisiting.       |
-- Worst Case of all cell = 1 so O(n*n) paths can be explored 

