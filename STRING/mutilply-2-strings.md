
# GEt :
- https://leetcode.com/problems/multiply-strings/
```cpp
class Solution {
public:
    string multiply(string num1, string num2) {
        if (num1 == "0" || num2 == "0") return "0" ;
        int n = num1.length() ;
        int m = num2.length() ;
        vector<int> res(n+m , 0) ;

        for (int i = n-1 ; i >= 0 ; i--){
            int d1 = num1[i] - '0' ;
            for (int j = m-1 ; j >= 0 ; j--){
                int d2 = num2[j] - '0' ;
                int sum = res[i+j+1] + d1 *d2 ;
                res[i+j+1] = sum % 10 ; 
                res[i+j] += sum / 10 ;
            }
        }
        string ans = "" ;
        int i = 0 ;
        while (i < res.size() && res[i] == 0) i++ ;
        for ( ; i < res.size() ; i++) {
            ans.push_back((char)(res[i] + '0'));
        }

        return ans.empty() ? "0" : ans ;
    }
};
```
