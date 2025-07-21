## Unique - Number - II

### INTUITION :
- We get the xor of 2 uniques, if we xor all elements (as all others in pairs cancels out )
- The rightMost set bit of XOR value of the 2 uniques say (a,b) will be such that one of them be having 1 bit & the other be having 0- bit at that position as XOR = a^b
- Now partition the array in 2 halfves , nums with set bit at that pos & nums without set bit at that pos then xor groups individually !
  
``` cpp
class Solution {
  public:
    vector<int> singleNum(vector<int>& arr) {
      
        int XOR = 0 ;
        for (int num: arr) XOR ^= num ;
        
        int  diffBit = (XOR&(-XOR)) ;
        
        int a = 0 , b = 0 ;
        for (int num : arr) {
            if (diffBit&num) {
                a ^= num ;
            }else {
                b ^= num ;
            }
        }
        if (b < a) return vector<int>{b,a} ;
        
        return  vector<int>{a,b} ;
    }
};
```


# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N)     |  Two time traversal of nums|
| 🧠 SPACE | O(1)       |  Only integers used as bitMask , unlike any datastructure |
