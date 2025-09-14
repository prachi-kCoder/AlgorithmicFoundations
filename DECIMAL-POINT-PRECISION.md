# DECIMAL-POINT-PRECISION

- In c++ decision point precised value are not printed by default even if you take the `num` {double type} as divisions or printing `cout` does their own rounding
## DISPLAY PREICISE
- Use `iomanip`  `setprecision(6)` upto any decimal places
```
#include<iomanip>
#include<iostream>
using namespace std ;
int main(){
  int n1 = 100 ; int n2 = 3 ;
  double val = static_cast<double>(n1)/n2 ;
// as cout trim value specially non-zero or small decimal values by default
  cout << fixed << setprecision(6) << val << endl ;
}
```

## To `return` and precisied values upto a certain deciaml point
```
#include<iostream>
using namespace std ;
double solve(int n1 , int n2) {
  double res = static_cast<double>(n1)/n2;
  return round(res*1e6) / 1e6 ; // here you mulitply with 10^6 then round it off for precision and then again divide with 10^6
}
int main() {
  int n1 = 100 ; int n2 = 3 ;
  double res = solve(n1 , n2) ;
   cout << fixed << setprecision(6) << res << endl ;
}
```
