# GAME-2-Players

- In this ques rather than thinking of getting the max score of player1 think of creating the max diff = player1 - player2 ,
- Try to maximise this , as both player are playing optimally hence on both the turn they 're optimally playing
- While this optimal play get the max_diff = dp[l][r][player]  , this states the max of val = score (p1) - score (p2)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
ll dp[5000][5000][2] ;
ll solve(int l , int r , vector<ll>& sc , int pl) {
    if (l == r) {
        return sc[l] ;
    }
    if (dp[l][r][pl] != -1) return dp[l][r][pl] ;
    
    ll sc1 = sc[l] ;
    ll nxt_1 = solve(l + 1 , r , sc , (1^pl));
    
    // get the the nxt player's score mini possible and you own score mx
    ll sc2 = sc[r] ;
    ll nxt_2 = solve(l , r-1 , sc , (1^pl));
    
    return dp[l][r][pl] = max(sc1 - nxt_1 , sc2 - nxt_2) ;
}
int main() {
    ll n ;
    cin >> n ;
    vector<ll> sc(n) ;
    ll total = 0LL ;
    for (int i = 0; i <n ; i++) {
        cin >> sc[i] ;
        total = total + sc[i] ;
    }
    if (n == 1) {
        cout << sc[0] << endl ;
        return 0 ;
    }
    memset(dp , -1 , sizeof(dp)) ;
    ll diff = solve(0 , n-1 , sc, 0) ;// mx diff
    
    cout << (total + diff)/2  << endl ;
    
    return 0 ;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N  x N x 2)        | We compute dp[l][r][player] for all subarrays [l, r] and both players. Each state depends on two recursive calls, and there are ~𝑁^2×2 total states. |
| 🧠 SPACE |   O( N x N x 2)         |          DP TABLE  |
