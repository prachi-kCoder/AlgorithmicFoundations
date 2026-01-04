# EUCLIDEAN ALGO :
- MODERN EUCLIDEAN : `gcd(a,b) = gcd(b , a%b) ` 
- TC : O(log(min(a,b))) very fast

- ORIGINAL (SUB-BASED) : `gcd(a,b) = gcd(a-b, b)` where (a>b)
- TC : O(max(a,b)) in worst case if a = 10^9 , b=1 then 10^9 subtraction & recusive calls giving TLE

- BUILT IN #include <numeric>
- use the gcd(a,b)  built in function
```
#include <numeric> // Required header
ll result = std::gcd(a, b);
```


```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
ll gcd(ll a , ll b) {
    if (b == 0) return a ;
    return gcd(b , a%b) ;
}
// if % is not allowed
ll gcd2(ll a , ll b) {
    if (a == b) return a ;
    return a > b ? gcd2(a - b , b) : gcd2(a , b-a);
}
int main() {
	// your code goes here
	ll a , b ;
	cin >> a >> b ;
	cout << gcd(a , b) << endl ;
	cout << gcd2(a , b) << endl ;
	
	return  0 ;
}

```
