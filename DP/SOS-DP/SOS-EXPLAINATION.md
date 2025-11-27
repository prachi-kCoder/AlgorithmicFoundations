# SOS-DP SUM OVER SUBSETS - DP

- ✔ Sum over all submasks of a mask : `g[mask] = Σ f[submask] for all (submask ⊆ mask)` 
- ✔ Sum over all supermasks of a mask : `g[mask] = Σ f[supermask] for all (mask ⊆ supermask)`

🔎 Brute Force Approach :
 - to compute  : `g[mask] = Σ f[submask] for all (submask ⊆ mask)`
 - For each mask (there are 2^𝑛 masks if we have 𝑛 bits), we need to iterate over all its submasks.
 - A mask of size 𝑛 can have up to 2^𝑛 submasks. So brute force complexity: `O (2^n . 2^n) = O(4^n)`

 🌀 Smarter Enumeration → O(3^𝑛)
 - Instead of looping over all masks and then all submasks, you can directly enumerate pairs (mask, submask) where 𝑠𝑢𝑏𝑚𝑎𝑠𝑘⊆𝑚𝑎𝑠𝑘.
 
- Each bit has 3 choices:
- Present in mask but not in submask
- Present in both mask and submask
- Absent in mask (and thus absent in submask)
  
 So total pairs = 3^n

- ⚡ SOS DP Optimization → O(N . 2^N)
The key insight of SOS DP is to reuse results by propagating contributions bit by bit:
- Instead of recomputing sums for each mask independently, we build them incrementally.
- For each bit position, we update DP values by transferring contributions from smaller masks to larger ones (or vice versa).
- 𝑂 (𝑛⋅2^𝑛)


- NOW a simple trick to get the compliment of any a[i] we use ((MAXN-1)^a[i]) as (MAXN-1)  is all 1 bits binary representation and ^ of a[i] with that gives compliment of a[i]

3. Why are "forward1" and "forward2" required?
- Standard SOS DP uses two fundamental transitions:
## ⭐ Forward 1: Subset → Superset DP
```
dp[mask] = sum of dp[submask] for all submask ⊆ mask
```
```cpp
void forward1(ll dp[]) {
    for (int bit = 0; bit < LOG ; bit++) {
        for (int i = 0; i < MAXN ;i++) {// all nums 
            if (i&(1<<bit)) {
                dp[i] += dp[i^(1<<bit)]; 
 }}}}
```
```
### 📌 Why this works:
- At  bit, if a mask i has that bit ON, then:
  i^(1<<bit) is the same mask but with that bit OFF
  all submasks that do not include this bit are already counted in dp[i^(1<<bit)]

So you add that to dp[i].
📌 Why is there no overcounting?
Because each submask covers a unique path of turning OFF bits from i.
For each submask → exactly one path of transitions.
```
### ⭐ forward2 = “Superset → Subset” DP
```
dp[mask] = sum of dp[supermask] for all supermask ⊇ mask
```
```cpp
void forward2(ll dp[]) {
    for (int bit = 0 ; bit < LOG ; bit++) {
        for (int i = 0 ; i < MAXN ;i++) {
            if (i&(1<<bit)) {
                dp[i^(1<<bit)] += dp[i] ;
            }}}}
```
```
📌 Why this works:
If i has a bit ON:
“smaller mask” = i^(1<<bit)
Any superset of the smaller mask that includes this bit must be i.
📌 Why is there no overcounting?
Because every superset relationship is walked once along each bit.
Each superset reduces to a smaller mask in exactly one way for each bit → no double counting.
```


# FOR CSES - BIT SOS DP PROBLEM :
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll LOG = 20; // all bit pos 2x10^6 
const ll MAXN = (1<<LOG) ;
    // subset counted to superset 
void forward1(ll dp[]) {
    for (int bit = 0; bit < LOG ; bit++) {
        for (int i = 0; i < MAXN ;i++) {// all nums 
            if (i&(1<<bit)) {
                dp[i] += dp[i^(1<<bit)]; 
            }
        }
        
    }
}
// superset cnt to subsets 
void forward2(ll dp[]) {
    for (int bit = 0 ; bit < LOG ; bit++) {
        for (int i = 0 ; i < MAXN ;i++) {
            if (i&(1<<bit)) {
                dp[i^(1<<bit)] += dp[i] ;
            }
        }
    }
}
ll freq1[MAXN];
ll freq2[MAXN];
int main() {
    ll n ;
    cin >> n ;
    int a[n] ;
    for (int i = 0; i < n ; i++) {
        cin >> a[i] ;
        freq1[a[i]]++;
        freq2[a[i]]++;
    }
    // to get x|y=x : ie all elements y which are subset of x 
    // to get x&y = x : ie all elements y which are superset of x 
    // to get those x&y != 0 ie N - (x&y=0) 
    forward1(freq1); // subsets updated
    forward2(freq2); // supersets updated 
    for (int i = 0; i < n ;i++) {
        ll a1 = freq1[a[i]] ;
        ll a2 = freq2[a[i]] ;
        ll negx = ((MAXN-1)^a[i]) ;
        ll a3 = n - freq1[negx]  ;
        cout << a1 <<" " << a2 << " " << a3 << "\n" ;
    }
    
    return 0 ;
}

```
