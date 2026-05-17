# Safe expo 
- To handle cases when taking mod is not explicitly mentioned and huge nums can give RuntimeError ! -> exceeding llong int as well !
- Make a safe_acceptable `LIMIT` , then if res -> every goes beyond it , or base `obly if next expo is necessary is going out of limits`
  
- Check : https://leetcode.com/problems/count-k-th-roots-in-a-range/description/
```cpp
ll safe_expo(ll base , ll expo , ll limit) {

        if (base == 0) return 0 ;
        if (expo == 0 ) return 1LL ;

        if (base > limit && expo > 1) return limit + 1  ;

        ll res = 1LL ;

        while (expo > 0) {
            if (expo&1) {
                if (res > limit / base ) return limit + 1 ;
                res = 1LL * res * base  ;
            }

            expo >>= 1 ;
            if (expo > 0) { // casefull here {only if expo > 0 then only limit+1 is a problem !}
                if (base > limit / base ) base = limit + 1 ;
                else base = 1LL * base * base ;
            }
        }

        return res ;
    }
```
