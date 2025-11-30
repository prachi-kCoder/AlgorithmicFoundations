# WildCard-Valid-Parenthesis

-> do here:https://leetcode.com/problems/valid-parenthesis-string/
- INTUITION :
```
- Keep track of lowest lowest `(` or highest `(` required for matching
- `*` can be empty ( or ) then obviously only return false in 2 scenarios :
-  ie the atleast lowest possible `(` is matching all `)` closing ones ie NO EXTRA `(` is left unmatched
- Or highest possible `(` is not  enough to matching all `)` , ie NO extra `)` are comming at any where in string where `(` and `*` together can't nullify it at anythime all throughout the string.
```
```
low = the minimum number of unmatched ( possible so far.
high = the maximum number of unmatched ( possible so far.

- If high < 0 → invalid (too many ))
- low = 0 then min cnt of ( all matched !
```
```cpp
bool checkValidString(string s) {
        int low = 0 , high = 0 ;

        for (char c : s) {
            if (c == '(') {
                low++ ;
                high++ ;
            }else if (c == ')') {
                if (low >0) low-- ;
                high-- ;
            }else {
                if (low >0) low-- ;
                high++ ;
            }
            if (high < 0) {
                return false ;
            }
        }

        return low == 0 ;
    }
```
