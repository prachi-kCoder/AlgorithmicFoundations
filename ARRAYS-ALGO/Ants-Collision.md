# ANTS-COLLSION

- Give it a try :https://www.geeksforgeeks.org/problems/last-moment-before-all-ants-fall-out-of-a-plank/1
- Trust me its easy again try it.

`Hint : Collision of 2 ants is equivalent to 2 ants passing each other , don't make it complex simulating collsion`
- `Eg : 0 1 2 3 4   consider A1 going RHS {at pos = 1} and A2 {at pos=2} going LHS  , on collision at time = 2 {again 1 ant at pos 1 & other at pos 2} isn't it the same scenario if they don't really collide and just pass each other`

```cpp
class Solution {
  public:
    int getLastMoment(int n, vector<int>& left, vector<int>& right) {
        // code here
        // we won't consider any collision as collision is as same as the 
        // 2 ants collide & reverse is equivalent to 2 ants pass each other
        
        // get the max time of any any 
        int mx = 0;
        for (int l : left) {
            mx = max( mx,l) ;
        }
        for (int r : right) {
            mx = max(mx , n-r) ;
        }
        
        return mx ;
        
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N)           |       Check max time of all timings  for all ants   |
| 🧠 SPACE |  O(1)          |    No extra space |
