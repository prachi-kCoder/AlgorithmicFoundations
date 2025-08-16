## SubsetII (Level-Rec-BackTracking) 

```cpp
class Solution {
public:
    void level_backtrack(int start , vector<int>& nums, vector<int>& curr , vector<vector<int>>& ans) {
        ans.push_back(curr) ;
      
        for (int i = start ; i < nums.size() ; i++ ) {
            if (i > start && nums[i] == nums[i-1]) continue ;
            curr.push_back(nums[i]);
            level_backtrack(i + 1 , nums , curr , ans) ;
            curr.pop_back();
        }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin() , nums.end()) ;
        vector<vector<int>> ans ;
        vector<int> curr ;
        level_backtrack(0 , nums, curr , ans) ;
        return ans ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(2^N*N)       |  Worst Case : When no duplicates hence all subsets are expored , TotalSubsets : O(2^N) ,each subset of n element |
| 🧠 SPACE | O(2^N* N )   | All subsets + recusion stack O(n)           |
