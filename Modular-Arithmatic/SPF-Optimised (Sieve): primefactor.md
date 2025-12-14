# SPF-Optimised (Sieve) :

- in Standard Sieve : {Take space upto O(N) and then to get the prime factor we take another O(SQRT(N))}
- Optimisd way is to use `SPF {Smallest Prime Factor of i}`
- that is rather that is_prime array of sieve we record the smallest prime of any ith number
  |---------|---|---|--|---|---|---|---|---|---|----|----|---|----|---|---|
  |Index(i) | 1 | 2 | 3| 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13| 14| 15|
  |SPF[I]  | 1 | 2 | 3 | 2 | 5 | 2 | 7 | 2 | 3 | 2 | 11 | 2 | 13 | 2 | 3 |

`  So for prime nums : SPF[I] = i `
and for composites SPF[i] = smallest prime divisors .
```
- EG  num = 60
SPF[60] = 2
then divigde 60/2 -> 30 -> 15
SPF[15] = 3
then divide 15/3 -> 5
SPF[5] = 5
then divide 5/5 -> 1
So the prime factors involved  {2,3,5} and you can also compute the power of thse by repeatedly adding the cnt and storing in map
````

## 2 RULE TO KEEP IN MIND 
## RULES OF COMPOSITES :
- Every composite number N will surely have atlest one prime factor p such that p <= sqrt(n)
- So to update the SPF of composite numbers we need to go upto sqrt(N) only
- All prime factor {will update larger multiples of them as spf[j] = i} where i-> SPF and j-> larger number

### SECOND 
- only SPF {IE SMALLEST PRIME FACTOR is enough to reach another factor }

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAX_N = 1e6 + 5 ;
int spf[MAX_N] ;
void sieve() {
    iota(spf , spf + MAX_N , 0) ; // ie spf[i] = i (init)
    
    for (int i = 2 ; i * i < MAX_N ; i++) {
        if (spf[i] == i) {// ie prime
            for (int j = i*i ; j < MAX_N ; j += i) {
                if (spf[j] == j) {
                    spf[j] = i ;// spf marked 
                }   
            } 
        }
    }
}
map<int,int> factorise(int x) {
    map<int,int> prime ;// and exponents
    
    while (x > 1) {
        int pf = spf[x] ;
        int expo = 0 ;
        while (x % pf == 0) {
            expo++ ;
            x /= pf ;
        }
        prime[pf] = expo ;
    }
    
    return prime ;
}
int main() {
    ios_base::sync_with_stdio(false); cin.tie(NULL);
    sieve();
    
    int x = 360 ;
    map<int,int> pf = factorise(x) ;
    for (auto &[fac, expo]: pf) {
        cout << "("<< fac << ":" << expo << ")" <<endl ;
    }
    
    return 0;

}

```
