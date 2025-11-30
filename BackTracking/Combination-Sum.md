# COMBINATION - SUM 
- Try achieveing the target with different combinations of numbers in your set
- https://leetcode.com/problems/combination-sum/description/
  
```cpp
class Solution {
public:
    vector<vector<int>> res;
    void solve(int i , int target , vector<int>& combination , vector<int>& candidates) {
        if (target == 0) {
            res.push_back(combination);
            return ;
        }
        if (i >= candidates.size()) return  ;
        if (candidates[i] > target) return ;// as candidates are sorted 

        if (candidates[i] <= target) {
            combination.push_back(candidates[i]) ;
            solve(i , target - candidates[i] , combination , candidates) ;
            combination.pop_back();
        }
        solve(i+1 , target, combination , candidates) ; 
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int> curr ;
        sort(candidates.begin() , candidates.end());

        solve(0 , target , curr , candidates ) ;
        return res ;
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(2^k ) | For all N : {Binary choices : Include / Skip and go to the next} , MaxDepth : Target/min(candidates[i]) as minElement can be called mulitple times to make the target giving the worst case of k depth |
| 🧠 SPACE | O( k ) | Recursion Stack  |

