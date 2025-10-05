## HOUSE-ROBBER

-- Keeping in mind  : Possibility of skipping at any house is necessary to globally maximise the sum 
```
class Solution {
  public:
    int n ;
    int solve(int i ,vector<int>& arr , int rob , vector<vector<int>>& dp) {
        if (i >= n) return 0 ;
        if (dp[i][rob] != -1) return dp[i][rob] ;
        
        int val = 0 ;
        
        if (rob) {// can rob!
            val = arr[i] + solve(i+1 ,arr , 0 , dp) ;
        }
        val = max(val ,solve(i+1 ,arr , 1 , dp)) ;// skipped curr 
        
        return dp[i][rob] = val ;
    }
    int findMaxSum(vector<int>& arr) {
        // code here
        n = arr.size();
        vector<vector<int>> dp(n, vector<int>(2 ,-1)) ;
        
        return max(solve(0, arr,0 , dp), solve(0 ,arr , 1, dp)) ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |               |           |
| 🧠 SPACE |            |            |
