
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long

const int LOG = 20;
const int MAXN = (1 << LOG);

ll freq[MAXN];

void forward1() {
    for (int bit = 0; bit < LOG; bit++) {
        for (int mask = 0; mask < MAXN; mask++) {
            if (mask & (1 << bit)) {
                freq[mask] += freq[mask ^ (1 << bit)];
            }
        }
    }
}

int main() {
    int mask;
    cin >> mask;

    // Mark all submasks of mask with weight = 1
    for (int sub = mask; ; sub = (sub - 1) & mask) {
        freq[sub] = 1;
        if (sub == 0) break;
    }

    // Run SOS DP
    forward1();

    // freq[mask] = number of submasks
    cout << freq[mask] << endl;

    return 0;
}

```
