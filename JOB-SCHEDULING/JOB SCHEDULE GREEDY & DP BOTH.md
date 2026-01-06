## JOB SCHEDULE GREEDY & DP BOTH
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> par ;
void init(int t) {
    par.resize(t+1 , 0) ;
    for (int i = 1 ; i <= t ; i++) par[i] = i ;
}
int find(int t) {
    if (par[t] == t) return t ;
    return par[t] = find(par[t]) ;
}
int max_profit (vector<int>& deadline , vector<int>& profit) {
    int n = deadline.size() ;
    vector<vector<int>> jobs(n, vector<int>(2)) ;
    for (int i = 0 ;i < n ; i++) {
        jobs[i][0] = profit[i] ;
        jobs[i][1] = deadline[i] ;
    }
    sort(jobs.rbegin() , jobs.rend()) ;
    int total = 0 ;
    int mxd = *max_element(deadline.begin() , deadline.end()) ;
    init(mxd) ;
    
    for (int i = 0 ; i < n ; i++ ) {
        int pro = jobs[i][0] ;
        int dead = jobs[i][1] ;
        int available_slot = find(dead) ;
        if (available_slot > 0) {
            total += pro ;
            par[available_slot] = find(available_slot-1) ;
        }
    }
    
    return total ;
}
// dp job scheduling
int max_profit_job_sch(vector<int>& start , vector<int>& end , vector<int>& profit) {
    int total = 0 ;
    int n = start.size() ;
    vector<vector<int>> jobs(n, vector<int>(3)) ;
    for (int i = 0 ;i < n ; i++) {
        jobs[i][0] = start[i] ;
        jobs[i][1] = end[i] ;
        jobs[i][2] = profit[i] ;
    }
    sort(jobs.begin() , jobs.end()) ;
    
    vector<int> dp (n+1 , 0) ;// dp[i]-> mx profit i get from the suffix 
    for (int i = n-1 ; i >= 0 ; i-- ) {
        int curr_start = jobs[i][0] ;
        int curr_end = jobs[i][1] ;
        int curr_profit = jobs[i][2] ;
        
        int low = i+1 ; int high = n-1 ;
        int safe = n ;
        while (low <= high) {
            int mid = low + (high - low)/2 ;
            if (jobs[mid][0] >= curr_end) {
                safe = mid ;
                high = mid - 1 ;
            }else {
                low = mid + 1 ;
            }
        }
        int include = curr_profit + dp[safe] ;
        int exclude = dp[i+1] ;
        dp[i] = max(include  , exclude);
    }
    
    return dp[0] ;
}
// activity selection for max cnt of jobs 
int max_activity(vector<int>&  st , vector<int>& end ) {
    vector<vector<int>> act ;
    int n = st.size() ;
    for (int i = 0 ; i < n ; i++) {
        act.push_back({st[i] , end[i]}) ;
    }
    sort(act.begin() , act.end() , [&](const vector<int>& a , const vector<int>& b) {
        return a[1] < b[1] ;
    }) ;// based on end time 
    int c = 0 ; int timer = -1 ;
    for (int i = 0 ; i < n ; i ++) {
        if (st[i] >= timer) {
            timer = max(end[i] , timer) ;
            c++ ;
        }
    }
    return c ;
}
int main() {
	// your code goes here

}

```
