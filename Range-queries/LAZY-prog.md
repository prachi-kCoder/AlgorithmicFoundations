# LAZY - PROPAGATION
- Keep in mind
- `RANGE - SUM + RANGE - UPDATES` : Both are possible only if the queries are made after push
- 2 times push() before & after the range is necessary !
- DO : https://codeforces.com/contest/52/problem/C

- Here is was for circular so handles {l, n-1} {0 , r} separately !
```cpp
#include <bits/stdc++.h>
#include <string>
// #include <ext/pb_ds/assoc_container.hpp>
// #include <ext/pb_ds/tree_policy.hpp>
using namespace std;
// using namespace __gnu_pbds;
#define IO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
#define ll long long
#define pll pair<ll,ll>
#define F first
#define S second
#define inf 1e18
const ll mod = (ll)1e9 + 7 ;
// #define Oset tree<int, null_type, less<int>, rb_tree_tag, tree_order_statistics_node_update>
struct SegTree {
    vector<ll> tree , lazy ;
    ll n ; 
  
    SegTree(vector<ll>& a ) {
      n = a.size();
      tree.resize(4*n , inf) ; lazy.resize(4*n , 0) ;
      
      build(0 , n-1 , a , 0) ;
    }
    
    void build(ll si , ll ei , vector<ll>& a , ll idx) {
        if (si == ei) {
            tree[idx] =  a[si] ;
            return ;
        }
        
        ll mid = si + (ei-si)/2;
        build(si , mid , a , 2*idx + 1) ;
        build(mid+1 , ei , a , 2*idx + 2) ;
        tree[idx] = min(tree[2*idx+1] , tree[2*idx+2]) ;
    }
    void push(ll idx , ll si , ll ei) {
        if (lazy[idx] != 0) {
            tree[idx] += lazy[idx] ; // update every level!
            if (si != ei) {
                lazy[2*idx + 1] += lazy[idx] ;  // add to values ! ie increse 
                lazy[2*idx + 2] += lazy[idx] ;
            }
            lazy[idx] = 0 ;
        }
    }
    ll query(ll si , ll ei , ll ql , ll qr , ll idx) {
        push(idx , si , ei) ; 
        
        if (si > qr || ei < ql) return inf;
    
        if (si >= ql && ei <= qr) {
            return tree[idx];
        }
        
        ll mid = (si + ei)/2;
        return min(
            query(si , mid , ql , qr , 2*idx + 1),
            query(mid+1 , ei , ql , qr , 2*idx + 2)
        );
    }
    void update(ll si, ll ei, ll ql, ll qr, ll idx, ll delta) {
        push(idx, si, ei);  // Push FIRST before processing
        
        if (si > qr || ei < ql) return;
        if (si >= ql && ei <= qr) {
            lazy[idx] += delta;
            push(idx, si, ei);  // Then push again to update
            return;
        }
        ll mid = si + (ei - si)/2;
        update(si, mid, ql, qr, 2*idx+1, delta);
        update(mid+1, ei, ql, qr, 2*idx+2, delta);
        tree[idx] = min(tree[2*idx+1], tree[2*idx+2]);
    }

    ll query(ll ql  , ll qr ) {
        if (ql <= qr) {
            return query(0, n-1 , ql , qr , 0 ) ;
        }else {
            ll last = query(0 , n-1 , ql , n-1 , 0 ) ;
            ll fro = query(0 , n-1 , 0 , qr , 0 ) ;
            return min(last , fro) ;
        }
    }
    void update(ll ql , ll qr , ll delta) {
        if (ql <= qr) {
            update(0 , n-1 , ql , qr , 0 , delta) ;

        }else {
            update(0 , n-1 , ql , n-1 , 0 , delta) ;
            update(0 , n-1 , 0 , qr , 0 , delta) ;
        }
    }
};
int main() {

        ll n ;
        cin >> n ;
        vector<ll> a(n) ;
        for (ll& e : a) cin >> e ;
        ll q ;
        cin >> q ;
        
        SegTree st(a);
        cin.ignore(); 
        
        for (ll i = 0 ;i < q ; i++) {
            string s ;
            getline(cin , s) ;
            stringstream ss(s) ;
            vector<ll> nums ;
            ll x ;
            while(ss >> x)  {
                // cout << x << "," ;
                nums.push_back(x) ;
            }
            // cout << endl ;
            
            ll lf = nums[0] , rg = nums[1] ;
            
            if (nums.size() == 3) {
                ll new_val = nums[2] ;
                st.update( lf , rg ,  new_val) ;
                
            }else {
                ll ans = st.query( lf , rg ) ;
                cout << ans << endl ;
            }
        }    
    return 0;
}
```
