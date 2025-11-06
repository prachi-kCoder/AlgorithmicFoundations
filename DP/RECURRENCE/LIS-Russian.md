## LIS 
- lis 2 variation : LIS Reconstruction & Russion Doll variation is important

- Do it first :https://leetcode.com/problems/russian-doll-envelopes/

- RUSSION DOLL ENV :
```cpp
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& env) {
        int n = env.size();
        sort(env.begin() , env.end(), [](const vector<int>& a, const vector<int>& b){
            return a[1] == b[1] ? a[0] > b[0] : a[1] < b[1] ;
        }) ;

        vector<int> wds ;
        for (auto& v : env) {
            wds.push_back(v[0]) ;
        }

        vector<int> lis_ends ;
        int m = wds.size() ;
        for (int i = 0 ; i < m ; i++) {
            auto it = lower_bound(lis_ends.begin() , lis_ends.end() , wds[i]);
            int j = it - lis_ends.begin() ;
            if (j >= lis_ends.size()) {
                lis_ends.push_back(wds[i]) ;
            } else {
                lis_ends[j] = min(lis_ends[j] , wds[i]) ;
            }
        }
        // for (int i = 0; i < env.size() ; i++) {
        //     cout <<"("<<env[i][0] << " " << env[i][1] << ") " ;
        // } 
        // cout << endl; 
        return lis_ends.size();
    }
};
```
TC : O(N log N)
