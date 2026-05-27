# PRIME-FACTORISATION
- Always check divisors up to sqrt(𝑛)  smaller prime factor only
- get the power computed , 
-  val > 1 -> prime check !,any prime left at the end !
  
```cpp
unordered_map<ll,ll> prime_fact(ll num) {
    unordered_map<ll,ll> pf;
    for (ll f = 2; f * f <= num; f++) {
        while (num % f == 0) {
            pf[f]++;
            num /= f;
        }
    }
    if (num > 1) pf[num]++;
    return pf;
}
```
