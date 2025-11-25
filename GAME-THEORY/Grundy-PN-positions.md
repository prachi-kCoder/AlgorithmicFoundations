## Grundy-PN-positions
```
The Grundy Value (Nimber): The Sprague-Grundy theorem generalizes this P/N concept using Grundy values (or Nimbers).
A state i is a P-position (LOSS) if and only if its Grundy value, G(i) :, is 0.
A state i is an N-position (WIN) if and only if its Grundy value, G(i), is non-zero.
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long

int main() {
    ll n; cin >> n;
    vector<int> grundy(n+1, 0);

    for (int i = 1; i <= n; i++) {
        set<int> s;
        for (int move = 1; move <= 3; move++) {
            if (i - move >= 0) s.insert(grundy[i - move]);
        }
        // mex calculation
        int g = 0;
        while (s.count(g)) g++;
        grundy[i] = g;
    }

    cout << "Grundy(" << n << ") = " << grundy[n] << "\n";
    if (grundy[n] == 0) cout << "P-position\n";
    else cout << "N-position\n";
}

```
