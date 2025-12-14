# SPF-Optimised (Sieve) :

- in Standard Sieve : {Take space upto O(N) and then to get the prime factor we take another O(SQRT(N))}
- Optimisd way is to use `SPF {Smallest Prime Factor of i}`
- that is rather that is_prime array of sieve we record the smallest prime of any ith number
  |--------------|----------------|
  |Index(i) | 1 | 2 | 3| 4| 5 | 6 |7 | 8| 9 | 10 | 11 | 12 | 13 | 14 | 15 |
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

```cpp

```
