# COMBINATION SUM 2
-https://leetcode.com/problems/combination-sum-ii/description/

- Take care of duplicate combination , only make unique combination
- Intuition to skip duplicates : **Recursive level based check**
- When we sort the input, duplicates appear adjacent. The goal is to prevent generating duplicate combinations—not duplicate values. We want:
          - ✅ [1,2,2] if it comes from one valid path
           - 🚫 but not [1,2,2] again from another path starting with the second 2
that make every index possible start and check for duplicates thereon forward ....
```cpp
class Solution {
public:
    void solve( int start , int curr_sum , int target , vector<int>& comb ,vector<int>& candidates, vector<vector<int>>& ans ) {
        if (curr_sum == target) {
            ans.push_back(comb) ;
            return  ;
        }
        int n = candidates.size();
    

        for (int i = start ; i < n ; i++){
            if (i > start && candidates[i-1] == candidates[i]) continue ;
            if (curr_sum + candidates[i] > target) break ;
            comb.push_back(candidates[i]) ;
            solve( i + 1 , curr_sum + candidates[i] , target , comb , candidates , ans) ;
            comb.pop_back();
        }
    }
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> ans ;
        int n =  candidates.size();
        sort(candidates.begin() , candidates.end()); // to skip for duplicate combination
        vector<int> comb ;
        solve(0 , 0 , target , comb ,candidates, ans) ;
        return ans ;
    }
};
```

# 🔍COMPLEXITY ANALYSIS

| METRIC   | COMPLEXITY   | WHY? |
|----------|--------------|------|
| 🧭 TIME  | O(2ⁿ)        | Each element can either be included or not, and sorting enables pruning via duplicates |
| 🧠 SPACE | O(n)         | Max recursion depth due to single-use constraint |
