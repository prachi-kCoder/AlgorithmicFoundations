# Job-Sequencing

#### "first solve it " : https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1?page=2&company=Amazon,Microsoft,Flipkart,Google&difficulty=Medium

- here greedily choosing one of the 2 parameters to sorte may not work
- As if we sort deadline {to do jobs with deadline closer, we may end up having lesser jobs , as this only works for the ques in which max no. of jobs is to be done {No intention for max profit}}
- & if we sort just based on profit : We may miss the jobs we could have done just because they were less profitable , and more profitable ones may have got more deadline so could have been delayed for better planning

- Simple Intuition is ,` DO the jobs with mx profit at a time closest to their deadline` ie {so that the jobs having less profit but closed deadline can also get the chance}
- Assign timeline based on this as every job is of `1 UNIT`

```cpp
class Solution {
  public:
    vector<int> jobSequencing(vector<int> &deadline, vector<int> &profit) {
        int n = deadline.size();

        int mx = 0 ;
        vector<pair<int,int>> v(n) ;
        for(int i = 0 ; i < n ; i++) {
            v[i].first = profit[i] ;
            v[i].second = deadline[i] ;
            mx = max(mx , deadline[i]) ;
        }
        sort(v.begin() , v.end() ,[](const pair<int,int>& a , const pair<int,int>& b){
            return a.first == b.first  ? a.second < b.second : a.first > b.first ;
        });
        vector<int> timeline(mx , 0) ;
        for (int i = 0 ;i  < mx ; i++) timeline[i] = i ;
        int total = 0 ;
        
        for (auto p : v) {
            int val = p.first ;
            int dead = p.second - 1 ; // 0th idex adjustment
            auto it = upper_bound(timeline.begin() , timeline.end() , dead) ;
            if (it == timeline.begin()) continue ;
            
            int idx = it - timeline.begin()-1 ;
            timeline.erase(timeline.begin() + idx);
            total += val ;
        }
        
        return {mx - timeline.size() , total} ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |       O(N*(LOG(mxt)))      | For n jobs , Binary Search over TimeLine of length = mx_time |
| 🧠 SPACE |      O(N) + O(MX)      | Vectorof pairs of jobs , time line array  |
`
