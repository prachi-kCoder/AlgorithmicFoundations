# BIN - PACKING

- try : https://leetcode.com/problems/minimum-number-of-work-sessions-to-finish-the-tasks/
- CSES : Elevator Rides {DP}

- - The concept is to pack all session of time / every interval with as much as busy as you could to optimally take lesser sessions of work , combining right set of tasks together with in a session to ie lesser overall no. of sessions are needed to complete all tasks .
  - BIN PACKING means : Packing the tasks well so that minimal session required
  - Most importantly : `Descending sort ` is necessary , because heavier task with more time consumption , make backtracking lighter with lesser possibilities to explore so backtracking tree is less bushy !
  - - If we start with small task in session huge possibilities are there and also its NP-Hard Problem as couldn't be solved in polynomial time!
    - Start with heavier task makes it efficient , lesser width / possibilities to explore !

```cpp
class Solution {
public:
    int ans ;
    void solve(int i , vector<int>& rem_time,vector<int>& task, int session_time) {
        if (i >= task.size()) {
            ans = min((int)rem_time.size() , ans) ;
            return ;
        }
        for (int j = 0; j < rem_time.size(); j++) {
            if (rem_time[j] >= task[i]) {
                rem_time[j] -= task[i] ;
                solve(i+1 , rem_time , task , session_time) ;
                rem_time[j] += task[i] ;
            }
        }

        rem_time.push_back(session_time - task[i]);
        solve(i+1 ,rem_time ,task , session_time) ;
        rem_time.pop_back();
    }
    int minSessions(vector<int>& tasks, int session_time) {
        int n = tasks.size();
        vector<int> rem_time;
        ans = n ;
        sort(tasks.begin() ,tasks.end());
        reverse(tasks.begin() ,tasks.end());
        
        solve(0 , rem_time ,tasks, session_time) ;
        return ans ;
    }
};

```
