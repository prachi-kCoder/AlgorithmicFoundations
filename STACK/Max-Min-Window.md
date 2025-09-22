# Max of min for every window size

- Try :https://www.geeksforgeeks.org/problems/maximum-of-minimum-for-every-window-size3453/1

- Here getting next smaller left and right gives us the right range for all element where they could be potentially the min
- Then for any ele to be min in a length `len` then obviously it could be the min of window size[1,len]
- Then max any val for the len possible
  
```
class Solution {
  public:
  vector<int> next_smaller(vector<int>& arr) {
      int n = arr.size();
      stack<int> stk ;
      
      vector<int> ns(n , n) ;
      for (int i = n-1 ; i >= 0 ; i-- ) {
          while (!stk.empty() && arr[i] <= arr[stk.top()]) {
              stk.pop();
          }
          if (!stk.empty()) {
              ns[i] = stk.top();
          }
          stk.push(i) ;
      }
      return ns;
  }
  vector<int> prev_smaller(vector<int>& arr) {
      int n = arr.size();
      stack<int> stk ;
      
      vector<int> ps(n , -1) ;
      for (int i = 0 ; i < n ; i++) {
          while (!stk.empty() && arr[i] <= arr[stk.top()]) {
              stk.pop();
          }
          if (!stk.empty()) {
              ps[i] = stk.top();
          }
          stk.push(i) ;
      }
      
      return ps;
  }
    vector<int> maxOfMins(vector<int>& arr) {
        //  code here
        int n = arr.size();
        vector<int> ns = next_smaller(arr) ;
        vector<int> ps = prev_smaller(arr) ;
        vector<int> res(n) ;
        
        for (int i = 0 ; i < n ; i++) {
            int len = ns[i] - ps[i] - 1 ;
            
            res[len-1] = max(res[len-1] , arr[i]) ;
        }
        for (int i = n-1 ; i > 0  ; i--) {
            res[i-1] = max(res[i] , res[i-1]) ;
        }
        return res ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(n)       |     as 4 traversals of all arr length n      |
| 🧠 SPACE |     O(N)       |   NEXTSMALLER LEFT AND NEXT SMALLER RIGHT         |
