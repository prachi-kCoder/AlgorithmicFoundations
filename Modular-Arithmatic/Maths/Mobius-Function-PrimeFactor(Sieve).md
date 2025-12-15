# Mobius-Function-PrimeFactor(Sieve)

## Möbius Function (denoted as mu(n)) is a mathematical tool that acts like a "switch" for the Inclusion-Exclusion Principle
- The function looks at the prime factorization of a number $n$ and assigns it one of three values: 1 , 0, -1
- 
- 
```cpp
#include <bits/stdc++.h>
using namespace std;

#define ll long long
const int MAX_VAL = 1e6 + 5;

// mu[i] stores the Mobius value for i
// cnt[i] stores how many numbers in the input are divisible by i
int mu[MAX_VAL];
int cnt[MAX_VAL];
vector<int> primes;
bool is_prime[MAX_VAL];

void sieve() {
    fill(is_prime , is_prime + MAX_VAL , true) ;
    is_prime[0] = is_prime[1] = false ;
    mu[1] = 1 ;
    
    for (ll i = 2 ; i < MAX_VAL ; i++){
        if (is_prime[i]) {
            primes.push_back(i) ;
            mu[i] = -1 ; // ODD cnt for mu[i] = -1 
        }
        for (int p : primes) {
            if (i * p >= MAX_VAL) break ;
            is_prime[i*p] = false ;
            
            if (i%p == 0) {
                mu[i * p] = 0; // Contains square factor (p*p)
                break;
            }else {
                mu[i * p] = -mu[i]; // Multiply by new prime, flip sign
            }
        }
    }
}

int main() {
    
        ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

        sieve();
    
        int n;
        cin >> n;
        
        for (int i = 0; i < n; i++) {
            int x;
            cin >> x;
            cnt[x]++;
        }
        // Step 2: Calculate how many numbers are multiples of 'i'
        for (ll i = 1 ; i < MAX_VAL ; i++) {
            for (ll j = i*2 ; j < MAX_VAL ; j+= i) {
                cnt[i] += cnt[j] ;
            }
        }
        
        // Step 3: Apply Mobius Inversion Formula
        ll valid_pairs = 0LL;
        for (ll i = 1 ; i < MAX_VAL ; i++) {
            if (mu[i] == 0) continue;
            // Number of pairs where both elements are multiples of i
            ll k = cnt[i] ;
            ll pairs = (1LL* k * (k-1))/2;
            if (mu[i] == 1) {
                valid_pairs += pairs; // inclusion
            } else {
                valid_pairs -= pairs; // exclusion
            }
        }
        
        cout<< valid_pairs << endl ;
    
    return 0;
    
}

```
