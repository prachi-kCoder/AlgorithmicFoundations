## Count of ZERO & PAIRS

### INTUTION :
```
`(a[i] & a[j]) == 0`
or say x&y = 0
iff y is a submask of ~x (within the bit-limit).
Because :
- If a bit is 1 in x: y must have 0 in that bit → fixed 0.
If a bit is 0 in x:
- y can freely have 0 or 1 → all combinations allowed.
This is exactly the set of submasks of:

  neg = (~x) masked into LOG bits
      = (MAXN-1) ^ x
count = sum of freq[submask of (~x)]


```
```cpp
const int LOG = 20;
const int MAXN = 1 << LOG;

long long freq[MAXN], g[MAXN];

void sos_submask_sum() {
    for (int mask = 0; mask < MAXN; mask++) g[mask] = freq[mask];
    for (int bit = 0; bit < LOG; bit++) {
        for (int mask = 0; mask < MAXN; mask++) {
            if (mask & (1 << bit)) {
                g[mask] += g[mask ^ (1 << bit)];
            }
        }
    }
}

long long count_and_zero_pairs(vector<int>& a) {
    for (int x : a) freq[x]++;

    sos_submask_sum();

    long long ans = 0;
    for (int x : a) {
        int negx = ((MAXN - 1) ^ x);
        ans += g[negx];
    }
    return ans;
}

```
