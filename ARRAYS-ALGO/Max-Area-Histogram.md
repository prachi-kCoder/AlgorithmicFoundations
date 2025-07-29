# Max-Area-Histogram

- Here we need the max area , which is only possible if i get continuously increasing heights , so that to maximise the width here comes the intuition of monotonic stack

 # METHOD 1 (2 pass)
 - Assume each height to be minimum and check how long towards left or right it can extend with all the heights >= currHt

```cpp
class Solution {
  public:
    vector<int> nextSmallerRight(vector<int>& arr) {
        int n = arr.size();
        vector<int> nsr(n, n) ;
        stack<int> stk ;
        for (int i = n-1 ; i>= 0 ; i--) {
            while (!stk.empty() && arr[i] <= arr[stk.top()]) {
                stk.pop();
            }
            if (!stk.empty()) {
                nsr[i] =  stk.top();
            }
            stk.push(i) ;
        }
        return nsr ;
    }
    vector<int> nextSmallerLeft(vector<int>& arr) {
        int n = arr.size();
        vector<int> nsl(n, -1) ;
        stack<int> stk ;
        for (int i = 0 ; i < n ; i++) {
            while (!stk.empty() && arr[i] <= arr[stk.top()]) {
                stk.pop();
            }
            if (!stk.empty()) {
                nsl[i] =  stk.top();
            }
            stk.push(i) ;
        }
        return nsl ;
    }
    int getMaxArea(vector<int> &arr) {
        
        int n = arr.size();
        vector<int> smLeft = nextSmallerLeft(arr) ;
        vector<int> smRight = nextSmallerRight(arr) ;
        int mxArea = 0 ;
        
        for (int i = 0; i < n ; i++) {
            int w = smRight[i] - smLeft[i] - 1 ;
            int area = arr[i]*w ;
            mxArea = max(mxArea, area) ;
        }
        return mxArea ;
    }
};

```
## METHOD 2 : MOST OPTIMISED :SINGLE PASS ON MONOTONIC STACK 
```cpp

```
