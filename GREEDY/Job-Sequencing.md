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

- MOST OPTIMISED :
- no erase function for timeline erase can be done to make it more optmal as erasing is expensive
```cpp
class Solution {
  public:
// DSU approach
    vector<int> par ;
    int find(int x ) {
        if (par[x] == x) return x ;// ie available slot
        return par[x] = find(par[x]) ;
    }
    void merge(int u , int v) { // to prev slot
        par[u] = v ;
    }
    vector<int> jobSequencing(vector<int>& deadline, vector<int>& profit) {
        int n = deadline.size();
        vector<pair<int,int>> jobs(n) ;
        int mx = 0 ;
        for (int i = 0 ; i < n ; i++) {
            jobs[i] = {profit[i] , deadline[i]} ;
            mx = max(mx , deadline[i]) ;
        }
        sort(jobs.begin() , jobs.end() , greater<>()) ;
        par.resize(mx+1) ;
        for (int i = 0; i <= mx ; i++) par[i] = i ;
        int cnt = 0 ;
        int total = 0 ;
        
        for (auto&[p , d] : jobs) {
            int slot = find(d) ;
            if (slot > 0)  {
                merge(slot , slot-1) ;
                cnt++;
                total += p ;
            }
            // no time <= x available!
        }
        
        return {cnt , total} ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*log(MX))  |  Sorting takes O(N log N); each job assignment uses DSU find() and merge() with nearly constant time due to path compression — governed by the inverse Ackermann function α(n), which grows extremely slowly  |
| 🧠 SPACE |    O(N + MX)        |  V {Job pairs} , Parent { latest available slot under the deadline} |
