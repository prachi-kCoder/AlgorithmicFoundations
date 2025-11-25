## Grundy-PN-positions

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
